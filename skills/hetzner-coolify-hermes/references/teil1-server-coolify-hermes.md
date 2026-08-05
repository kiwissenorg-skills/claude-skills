# TEIL 1 — Server + Coolify + Hermes (ohne Domains)
# 3x live getestet (10.06.2026). Reihenfolge strikt einhalten.

## 0) Zugangsdaten einsammeln
- Hetzner-API-Token (Read & Write — Read allein reicht NICHT).
- Coolify-Admin-E-Mail (vom Nutzer).
- Coolify-Admin-Passwort: selbst generieren nach der PASSWORT-REGEL unten.
- OpenRouter-Key: optional. Wenn leer → später nachtragen, Hermes antwortet erst dann.
- ROOT_USERNAME: ein Wort OHNE Leerzeichen (z.B. der Vorname).

### PASSWORT-REGEL (zwei Bedingungen gleichzeitig — Stolperfallen 3.1 + 3.11)
1. MUSS mind. ein Sonderzeichen enthalten, sonst lehnt Coolify ab und legt KEINEN
   Admin-User an → API 401. Empfohlene Symbole: ! _ - . # % + =
2. KEINE shell-/.env-brechenden Zeichen (Leerzeichen, $ " ' \ Backtick).
3. Passwort UND ROOT_USERNAME in der .env quoten.
Beispiel-Generator: 20 alphanumerische Zeichen + "!" + ein Symbol aus #%+=._-

## 1) SERVER-AUSWAHL (PFLICHT — niemals überspringen)
1. Live-Verfügbarkeit für ALLE Standorte abfragen:
   GET https://api.hetzner.cloud/v1/server_types  (Header: Authorization: Bearer <TOKEN>)
   GET https://api.hetzner.cloud/v1/datacenters
   Verfügbarkeit pro Standort = server_types.available je Datacenter.
2. Als Tabelle zeigen, Spalten: Typ | Kategorie (Generation) | CPU-Typ | vCPU | RAM |
   Disk | Preis/Monat | Nürnberg (nbg1) | Falkenstein (fsn1) | Helsinki (hel1).
   Kategorie aus API-Feld `category`:
     cost_optimized  = "Cost-Optimized (ältere Gen, limitiert)"
     regular_purpose = "Regular Performance (neuere AMD)"
     dedicated       = "General Purpose (dediziert)"
   Standorte ausgeschrieben. Generation NICHT weglassen.
   Fakt: cx32 ist deprecated; Nachfolger cx33 (günstig) bzw. cpx32 (neuere AMD, besser).
   Empfehlung für Hermes mit Browser-Tools: mind. 4 vCPU / 8 GB.
3. STOPP. Auf ausdrückliche Bestätigung warten: "ja, leg an: <typ> in <standort>".
   AUF KEINEN FALL vorher anlegen.

## 2) cloud-init bauen + Server anlegen
- SSH-Key erzeugen (ed25519), Public-Key bei Hetzner hochladen (POST /v1/ssh_keys).
- cloud-init (Ubuntu 24.04): Install-Skript via write_files ablegen, in runcmd nur
  aufrufen, Logging nach /var/log/coolify-install.log. Das Skript:
  * Coolify installieren (curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash)
    mit ENV ROOT_USERNAME / ROOT_USER_EMAIL / ROOT_USER_PASSWORD.
  * .env quoten (Stolperfalle 3.1): in /data/coolify/source/.env ROOT_USERNAME und
    ROOT_USER_PASSWORD in Anführungszeichen setzen.
  * SSH-Key NACH dem Install wieder anhängen (Stolperfalle 3.2): eigenen Public-Key
    idempotent (grep -qF) an /root/.ssh/authorized_keys, chmod 600,
    systemctl restart ssh sshd.
  * Auf coolify-db warten (pg_isready), dann:
  * ADMIN-USER ROBUST anlegen (Stolperfalle 3.11 — KRITISCH): docker restart lädt die
    geänderte .env NICHT neu. Daher Seed mit EXPLIZITER Env starten:
      docker exec -e ROOT_USERNAME="<name>" -e ROOT_USER_EMAIL="<mail>" \
        -e ROOT_USER_PASSWORD="<pw>" coolify php artisan db:seed \
        --class=RootUserSeeder --force
  * API aktivieren (3.4):
      docker exec coolify-db psql -U coolify -d coolify \
        -c "update instance_settings set is_api_enabled = true;"
  * API-Token DIREKT in die DB (3.5 — tinker scheitert an team_id):
      insert into personal_access_tokens (tokenable_type, tokenable_id, team_id, name,
        token, abilities, created_at, updated_at) values ('App\Models\User', 0, 0,
        'setup', '<sha256(plain)>', '["*"]', now(), now());
- Server anlegen: POST /v1/servers mit server_type=<gewählt>, image=ubuntu-24.04,
  location=<gewählt>, ssh_keys=[<id>], user_data=<cloud-init>, start_after_create=true.

## 3) HEALTH-POLLING (Perfektion vor Schnelligkeit)
- Boot bis Coolify gesund dauert ~5-6 Min. Alle 10s prüfen, max 30 Min:
  * Web: http://<IP>:8000 liefert 302
  * Container: alle coolify* "healthy" (docker ps)
  * API: GET http://<IP>:8000/api/v1/servers mit Bearer-Token = 200
- SELF-HEALING bei 500 (3.1): .env quoten + docker restart coolify, weiter pollen.

## 4) HERMES DEPLOYEN
- Server-UUID holen (GET /api/v1/servers), Projekt anlegen (POST /api/v1/projects).
- Service deployen: POST /api/v1/services mit type=hermes-agent-with-webui,
  project_uuid, environment_name=production, server_uuid, instant_deploy=true.
  Die Antwort liefert die sslip.io-URL (hermeswebui-<uuid>.<IP>.sslip.io:8787).
- WebUI-Passwort auslesen: SERVICE_PASSWORD_HERMESWEBUI aus
  /data/coolify/services/<service_uuid>/.env.
- OpenRouter-Key: wenn vorhanden → im Service setzen (OPENROUTER_API_KEY) + Restart;
  wenn leer → überspringen + am Ende Hinweis "antwortet erst nach Nachtrag".
- IP:Port-Zugriff (Stolperfalle 3.10): DB-Feld ports REICHT NICHT. Mapping "8787:8787"
  DIREKT ins generierte Compose unter hermes-webui (gleiche Ebene wie image), dann
  docker compose -f docker-compose.yml up -d. Ergebnis: 0.0.0.0:8787->8787/tcp.
  HINWEIS: redeploy-flüchtig — nach UI-Redeploy erneut patchen.

## 5) SELBST-TEST TEIL 1 (automatisch, mit Reparatur)
Führe diese Prüfungen aus. Bei Fehlschlag die Reparatur anwenden und erneut testen
(max. 3 Runden je Check), erst bei Grün weiter:

| Check | Erwartung | Reparatur bei Fehler |
|-------|-----------|----------------------|
| Coolify Web | curl http://IP:8000 → 302 | warten/pollen; bei 500 .env-Fix + restart coolify |
| Coolify API | GET /api/v1/servers → 200 | users-Tabelle leer? → RootUserSeeder mit -e Env neu (3.11); API disabled? → is_api_enabled=true |
| Hermes /health (intern) | curl 127.0.0.1:8787/health auf Server → 200 | Container neu: docker compose up -d im Service-Verzeichnis |
| Hermes IP:Port (extern) | curl http://IP:8787/health → 200 | ports-Mapping fehlt → ins Compose patchen (3.10) + up -d |
| Hermes sslip.io | curl http://hermeswebui-...sslip.io:8787/health → 200 | Service-Redeploy abwarten; Traefik-Labels prüfen |

## 6) STATE-DATEI schreiben (Brücke zu Teil 2)
Lege /root/hermes-state.json an (chmod 600) mit:
  version, created_at, provider_server="hetzner", server_id, server_ip, server_type,
  location, coolify{url, admin_email, api_token, server_uuid, instance_settings_id},
  hermes{project_uuid, service_uuid, webui_app_name="hermes-webui", webui_port=8787,
  webui_password, sslip_url, openrouter_set}, ssh{key_comment}.
Zusätzlich /root/ZUGANGSDATEN.txt menschenlesbar (Hinweis "nach Anleitung löschen").

## 7) ABSCHLUSS

### 7.0) PFLICHT: Passwörter verifizieren, BEVOR sie ausgegeben werden (siehe SKILL.md-Regel)
Bevor du IRGENDEIN Passwort in die Abschluss-Antwort schreibst, lies den aktuellen Wert
frisch vom Server und teste den Login. Nenne ausschließlich den Wert, der den Test eben
bestanden hat. Niemals einen Wert aus dem Gedächtnis / aus einer früheren Variable.
- Coolify-Admin-Passwort:
    PW=$(ssh ... "grep '^ROOT_USER_PASSWORD=' /data/coolify/source/.env | cut -d= -f2- | tr -d '\"'")
    # Login real testen (z.B. /api/v1 mit Token ist 200; für PW selbst: Coolify-Login-POST
    # oder zumindest sicherstellen, dass exakt dieser .env-Wert genannt wird).
    # NUR diesen exakten $PW-String ausgeben.
- Hermes-WebUI-Passwort:
    WUI=$(ssh ... "grep '^SERVICE_PASSWORD_HERMESWEBUI=' /data/coolify/services/<svc>/.env | cut -d= -f2-")
    # NUR diesen exakten $WUI-String ausgeben.
- Übernimm die Werte direkt aus der Shell-Variable in die Ausgabe; tippe sie nicht ab.
  Schlägt eine Verifikation fehl -> NICHT raten: Wert neu setzen, erneut testen, dann ausgeben.

- Ausgeben: Server-IP, Coolify-URL+Login+Passwort, Hermes-WebUI (IP:Port UND sslip.io)
  + Passwort. Falls OpenRouter leer: deutlich sagen, dass Hermes erst nach Nachtrag antwortet.
- Kurz erklären, wie der Nutzer selbst testet: http://IP:8787 im Browser öffnen, einloggen.
- Sicherheit: Hetzner-Token rotieren/löschen, Coolify/Hermes-Passwörter nach erstem Login
  ändern, ZUGANGSDATEN.txt löschen, API ggf. wieder deaktivieren.
- Teardown anbieten (Server + SSH-Key löschen), nichts ohne Bestätigung; nur was in
  diesem Lauf angelegt wurde.
