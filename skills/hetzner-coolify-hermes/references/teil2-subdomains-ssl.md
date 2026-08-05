# TEIL 2 — Subdomains anbinden + automatisches SSL
# DNS-Schreiben (IONOS) und SSL-Kette live getestet (10.06.2026).
# Schlanke Variante: nur 2 Subdomains (Coolify + Hermes-WebUI). KEINE Dashboard-Subdomain.

## 0) Voraussetzungen + State laden
- Teil 1 abgeschlossen, Server läuft. /root/hermes-state.json per SSH lesen → daraus
  server_ip, coolify api_token, server_uuid, hermes service_uuid. So muss der
  Coolify-Token NICHT durch den Chat.
- Falls State-Datei fehlt (Server aus altem Lauf): Werte aus Coolify rekonstruieren
  (DB/API) — Fallback.
- Vom Nutzer: IONOS-DNS-Zugangsdaten + Domain.

## 1) Subdomains festlegen
Genau ZWEI Subdomains (Nutzer bestätigt/ändert die Namen):
  coolify.<domain>  → Coolify (Port 8000)
  hermes.<domain>   → Hermes WebUI (Port 8787)  ← die eigentliche Oberfläche

Bewusst KEINE dritte "dashboard-hermes"-Subdomain. Die WebUI ist die vollständige
Bedienoberfläche (inkl. Einstellungen über das "Hermes Control Center" in der WebUI).
Ein öffentlich exponiertes Dashboard ist unnötig und vergrößert nur die Angriffsfläche.
Wenn das offizielle Hermes-Dashboard wirklich gebraucht wird → optionaler SSH-Tunnel,
siehe Abschnitt 7 (standardmäßig NICHT einrichten).

## 2) VORAB-TEST DNS (vor jeder Änderung — wichtig!)
- Nameserver der Domain prüfen: dig +short NS <domain>. Die Domain muss IONOS-Nameserver
  nutzen, sonst greift die API nicht.
- Zonen-TTL prüfen (dig +short SOA <domain> → letzter Wert). Ist sie hoch (z.B. 86400),
  propagieren Änderungen langsam! Dann pro Record eine niedrige ttl (z.B. 300) setzen
  und den Nutzer auf mögliche Wartezeit hinweisen.
- WILDCARD prüfen: existiert ein "*"-Record? Er überlagert die Subdomains
  (live bestätigt). Dann mit dem Nutzer klären: Wildcard löschen oder umbiegen.
  Ohne Behandlung lösen coolify/hermes evtl. auf die Wildcard-IP auf → SSL scheitert.

## 3) A-Records setzen (Details + curl in references/dns-provider-api.md)
- Je Subdomain einen A-Record → server_ip, TTL niedrig (z.B. 300). Also zwei Records:
  coolify.<domain> und hermes.<domain>.
- IONOS: name = VOLLER FQDN.
- Idempotenz: existiert der Record schon → aktualisieren statt doppelt anlegen.

## 4) Auf Propagation warten (PFLICHT vor SSL)
- Pollen bis dig +short <sub>.<domain> == server_ip — und zwar an einem öffentlichen
  Resolver (1.1.1.1 / 8.8.8.8) UND am autoritativen NS. Erst dann weiter.
- Warum: Coolify/Traefik holt das Let's-Encrypt-Zertifikat selbst, aber Let's Encrypt
  prüft per HTTP, ob die Subdomain wirklich auf den Server zeigt. Zeigt DNS noch
  woandershin → LE schlägt fehl (Achtung LE-Rate-Limit: ~5 Fehlversuche/Stunde/Domain).
- IONOS propagiert schnell (frische Subdomain <1 Min).

## 5) Domains in Coolify setzen (Traefik zieht SSL automatisch)
- Coolify-eigene Domain (Stolperfalle 3.7):
    update instance_settings set fqdn='https://coolify.<domain>';
    docker exec coolify php artisan tinker --execute=
      "App\Models\Server::find(0)->setupDynamicProxyConfiguration();"
    docker restart coolify-proxy
- Hermes-WebUI-Domain (Stolperfalle 3.6):
    update service_applications set fqdn='https://hermes.<domain>' where name='hermes-webui';
    danach Service neu deployen (Labels neu: Host-Rule + HTTPS-Router + letsencrypt).
- WICHTIG: fqdn IMMER mit https:// (sonst non-Secure-Cookies → Login kaputt).

## 6) SELBST-TEST / SSL-VERIFIKATION (live bewiesenes Muster)
Pro Subdomain prüfen (nach kurzer Wartezeit, Traefik braucht ~30-60s):
  curl -I https://<sub>.<domain>   → 200/302
  openssl s_client -servername <sub> -connect <sub>:443 | openssl x509 -noout -issuer
    → issuer muss "Let's Encrypt" enthalten.
Bewährtes Ergebnis (Referenz): https://coolify.<domain> → 302, Issuer=Let's Encrypt;
https://hermes.<domain> → 200/302 (Login der WebUI).
Bei Fehler: DNS erneut prüfen (zeigt es wirklich auf den Server?), Traefik-Labels
prüfen, coolify-proxy neu starten, dann erneut testen.

## 7) OPTIONAL — offizielles Hermes-Dashboard NUR per SSH-Tunnel (nicht öffentlich)
Standardmäßig NICHT einrichten. Nur wenn der Nutzer das offizielle Nous-Dashboard
(Port 9119, z.B. für die Hermes-Desktop-App-Anbindung) ausdrücklich braucht.

Grundregel: **Das Dashboard NIE als öffentliche Subdomain exponieren.** Ein offen
erreichbares, unauthentifiziertes Dashboard war das Einfallstor der Juni-2026-Angriffs-
welle (Scanner trieben Agenten dazu, SSH-Backdoors zu setzen); `--insecure` wurde deshalb
entfernt. Der sichere, einfache Weg ist ein SSH-Tunnel — kein Auth-Proxy, kein
öffentlicher DNS-Record, kein Dauerbetrieb im Netz.

Vorgehen:
- Dashboard im Hermes-Agent-Container LOOPBACK-only starten (kein `--insecure`):
    docker exec -d <agent> sh -c 'hermes dashboard --host 127.0.0.1 --port 9119 \
      --no-open --skip-build >/tmp/dash.log 2>&1'
  (Fehlt das Subkommando: `pip install "hermes-agent[web,pty]"` im Container.)
- Auf dem Server das Container-Loopback auf einen Host-Port bringen (nur bei Bedarf), z.B.
  via `docker exec`-Portforward oder indem der Agent-Container den Port am Host mappt —
  am einfachsten aber: direkt vom eigenen Rechner tunneln.
- Vom eigenen Rechner tunneln und im Browser lokal öffnen:
    ssh -L 9119:127.0.0.1:9119 root@<server_ip>
    # danach im Browser: http://127.0.0.1:9119
  (Läuft das Dashboard im Container statt auf dem Host, im Tunnel-Ziel die Container-IP
  im Coolify-Netz verwenden, z.B. -L 9119:10.0.2.2:9119.)

Der Tunnel ist nur aktiv, solange die SSH-Verbindung steht — nichts bleibt öffentlich
erreichbar, keine Zusatz-URL, kein GATE-Passwort nötig (der Server-SSH-Zugang ist die Auth).

## 8) ABSCHLUSS

### 8.0) PFLICHT: Passwörter verifizieren, BEVOR sie genannt werden
Halte dich strikt an die Regel "PASSWORT-WAHRHEITSQUELLE" aus der SKILL.md: aktuellen
Wert frisch vom Server lesen, Login real testen, nur den getesteten Wert ausgeben.
Betroffen sind hier: Coolify-Admin und Hermes-WebUI. (Ein Dashboard-Gate-Passwort gibt
es in dieser schlanken Variante nicht mehr.)

- Alle HTTPS-URLs + Logins ausgeben (coolify.<domain>, hermes.<domain>).
- Kurz erklären: Bedienung läuft komplett über die WebUI (hermes.<domain>); Einstellungen
  im "Hermes Control Center" (Launcher unten in der Seitenleiste der WebUI).
- IONOS-Key zum Rotieren/Löschen empfehlen; Hetzner-Token rotieren/löschen; Coolify/Hermes-
  Passwörter nach erstem Login ändern.
- Falls jemand das offizielle Dashboard braucht: auf den SSH-Tunnel (Abschnitt 7)
  verweisen — NIE öffentlich exponieren.
- Teardown anbieten (nur in diesem Lauf Angelegtes; Serverliste vor dem Löschen zeigen).
