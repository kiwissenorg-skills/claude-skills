---
name: test
---

# Test [link](http://example.com) `code` "quotes" 'single' {braces}

```js
function f() { return [1,2,3]; }
```
---
name: hetzner-coolify-hermes
description: Installiert vollautomatisch einen Hetzner-Server mit Coolify und dem Hermes-Agenten (Agent + WebUI) und verbindet optional Subdomains via IONOS-DNS-API (inkl. automatischem Let's-Encrypt-SSL über Coolify). Die WebUI ist die einzige Oberfläche — kein zusätzliches Dashboard, keine dritte URL. Nutze diesen Skill IMMER wenn jemand Coolify, Hermes/Hermes-Agent, ein Self-Hosting-Setup oder einen Hetzner-Server aufsetzen will — auch bei Formulierungen wie "richte mir Coolify ein", "installier Hermes auf einem Server", "ich will einen eigenen Agenten hosten", "Coolify mit Domain", "Subdomain auf meinen Server verbinden", "Hetzner Server mit Coolify", "deploy hermes-agent-with-webui".
---

# Coolify + Hermes Deployer (schlank, ohne Dashboard-Subdomain)

Dieser Skill richtet auf Hetzner vollautomatisch Coolify und den Hermes-Agenten ein
und verbindet auf Wunsch Subdomains mit automatischem SSL. Er ist in zwei Phasen
aufgebaut, die durch eine **State-Datei** verbunden sind und jeweils einen
**eingebauten Selbst-Test mit Reparatur** haben:

- **TEIL 1** — Hetzner-Server anlegen, Coolify installieren, Hermes deployen (ohne Domains).
- **TEIL 2** — Subdomains via IONOS-DNS-API anbinden, SSL automatisch.

Das Leitprinzip: **Perfektion vor Schnelligkeit.** Lieber lange auf einen gesunden
Zustand warten und automatisch reparieren, als zu früh weitermachen. Jede Phase
endet erst, wenn ihr Selbst-Test grün ist.

## Genau ZWEI Oberflächen-URLs — bewusst KEIN separates Dashboard

Dieses Setup verbindet **nur zwei** Subdomains:

- `coolify.<domain>` → Coolify-Admin (Server/Deployments verwalten)
- `hermes.<domain>`  → **Hermes-WebUI** (deine eigentliche Oberfläche: Chat + Einstellungen)

Die **Hermes-WebUI ist die vollständige Bedienoberfläche.** Alle Einstellungen,
Sessions, Profile, das Passwort, Modelle und Werkzeuge liegen im **"Hermes Control
Center"** (Launcher unten in der Seitenleiste der WebUI). Ein zusätzliches, öffentlich
erreichbares Hermes-Dashboard (frühere dritte Subdomain `dashboard-hermes.<domain>`)
wird **bewusst NICHT** angelegt:

- Die WebUI deckt die tägliche Bedienung komplett ab → eine dritte URL ist überflüssig.
- Ein öffentlich exponiertes Dashboard war das Einfallstor der Juni-2026-Angriffswelle
  (Scanner trieben Agenten dazu, SSH-Backdoors zu setzen); Nous hat `--insecure` deshalb
  entfernt. Weniger öffentliche Angriffsfläche = sicherer.
- Kein selbstgebauter Auth-Proxy, kein systemd-Timer, kein GATE-Passwort → deutlich
  weniger bewegliche Teile und Fehlerquellen.

**Falls das offizielle Hermes-Dashboard doch einmal gebraucht wird** (z.B. für die
Hermes-Desktop-App-Anbindung): NIE als öffentliche Subdomain exponieren, sondern
**loopback-only starten und per SSH-Tunnel** erreichen. Der genaue Weg steht als
optionaler Anhang in `references/teil2-subdomains-ssl.md` (Abschnitt 7). Standardmäßig
wird das NICHT eingerichtet.

## Wichtige Sicherheitsregeln (immer beachten)

- **Niemals selbstständig einen Server anlegen.** Erst Verfügbarkeit zeigen, dann auf
  ausdrückliche Bestätigung von Typ UND Standort warten ("ja, leg an: <typ> in <standort>").
- **Secrets nie im Klartext ausgeben** und nie in Ausgabedateien schreiben. Den Nutzer
  darauf hinweisen, API-Tokens nach dem Setup zu rotieren/löschen.
- **Beim Teardown nie fremde/produktive Server anfassen** — nur, was in diesem Lauf
  angelegt wurde. Vor dem Löschen die Serverliste zeigen.

### 🔴 PASSWORT-WAHRHEITSQUELLE (ABSOLUTE REGEL — niemals brechen)
Jedes Passwort, das du dem Nutzer nennst, MUSS unmittelbar vorher gegen den laufenden
Server verifiziert worden sein. Die Wahrheit ist IMMER der Wert, der auf dem Server
aktiv ist — NIEMALS ein Wert aus deinem Gedächtnis, aus einer früheren Antwort, aus
einer lokalen Variable oder "der, den ich generiert habe".

Verbindliche Reihenfolge für JEDES Passwort (Coolify-Admin, Hermes-WebUI):
1. **Direkt vor der Ausgabe** den aktuell gültigen Wert aus der maßgeblichen Quelle lesen:
   - Coolify-Admin: aus `/data/coolify/source/.env` (ROOT_USER_PASSWORD).
   - Hermes-WebUI: aus der Service-.env (SERVICE_PASSWORD_HERMESWEBUI) bzw.
     `/root/hermes-state.json`.
2. **Login real testen** und das Ergebnis abwarten, BEVOR du das Passwort in die Antwort
   schreibst:
   - Coolify: Login bzw. /api/v1-Aufruf mit dem gelesenen Wert -> erwartetes 200/302.
   - Hermes-WebUI: Login mit dem gelesenen Wert -> erwarteter Erfolg.
3. **NUR den exakten String, mit dem der Login eben nachweislich geklappt hat**, ausgeben.
   Nicht abtippen, nicht aus dem Kopf — wortwörtlich denselben Wert verwenden, der den
   erfolgreichen Login erzeugt hat. Am sichersten: das Passwort direkt aus der Quelle in
   die Ausgabe übernehmen, nicht erneut eintippen.

Wenn der Verifikations-Login fehlschlägt: NICHT raten und NICHT irgendein Passwort
ausgeben. Stattdessen das Passwort auf dem Server neu setzen, erneut testen, und erst
nach erfolgreichem Test ausgeben.

Diese Regel existiert, weil in der Vergangenheit ein nicht-verifiziertes Passwort
genannt wurde, das nicht zum tatsächlich gesetzten Wert passte. Das darf nie wieder
passieren. Wenn du ein Passwort nicht frisch verifiziert hast, darfst du es NICHT nennen.

## Welche Phase?

- Will der Nutzer den Server/Coolify/Hermes neu aufsetzen → **TEIL 1** (lies
  `references/teil1-server-coolify-hermes.md`).
- Steht bereits ein Coolify/Hermes-Server und es sollen Subdomains dran → **TEIL 2**
  (lies `references/teil2-subdomains-ssl.md`).
- Beides nacheinander → TEIL 1, dann automatisch TEIL 2 (der State-Vertrag verbindet sie).

Frage den Nutzer am Anfang kurz, was er braucht und welche Zugangsdaten vorliegen,
und nutze dafür die AskUserQuestion-Möglichkeit, statt alles auf einmal zu verlangen.

## Benötigte Zugangsdaten (je nach Phase)

TEIL 1: Hetzner-API-Token (Read & Write). Optional OpenRouter-Key (kann später nach).
TEIL 2: IONOS-DNS-Zugangsdaten + die Domain.

So findet der Nutzer die Keys:
- Hetzner: console.hetzner.cloud → Projekt → Security → API-Tokens → Read & Write.
- IONOS: developer.hosting.ionos.DE (Inkognito, Hauptkonto) → Key = PREFIX.SECRET.

(Details und die genauen API-Aufrufe stehen in den reference-Dateien.)

## Ablauf auf hoher Ebene

1. Klären, welche Phase und welche Zugangsdaten da sind.
2. **TEIL 1** ausführen (siehe reference). Danach **Selbst-Test Teil 1**: Coolify-Login
   (302), API (200), Hermes /health (200). Bei Fehler automatisch reparieren (die
   reference beschreibt die bekannten Reparaturen) und erneut testen. Erst bei Grün weiter.
3. **State-Datei** `/root/hermes-state.json` auf dem Server schreiben (Schema in der
   reference). Sie ist die Brücke zu Teil 2.
4. Wenn Subdomains gewünscht: **TEIL 2** ausführen (siehe reference). Beginnt mit einem
   **Vorab-Test** (DNS erreichbar? Wildcard vorhanden? TTL?), setzt dann die zwei Records
   (coolify + hermes), wartet auf Propagation, setzt Coolify-FQDN, verifiziert SSL.
5. Abschluss: URLs + Logins ausgeben, Sicherheitshinweise, Teardown anbieten.

## Reference-Dateien

- `references/teil1-server-coolify-hermes.md` — Teil 1 komplett: Verfügbarkeit, cloud-init,
  alle Stolperfallen (3.1–3.11) mit Fixes, Hermes-Deploy, Selbst-Test, State-Datei.
- `references/teil2-subdomains-ssl.md` — Teil 2 komplett: IONOS-API (live
  getestete Aufrufe), Wildcard/TTL-Behandlung, Coolify-FQDN und Hermes-WebUI-FQDN,
  SSL-Verifikation. Enthält als **optionalen Anhang (Abschnitt 7)** den sicheren
  SSH-Tunnel-Weg zum offiziellen Dashboard — standardmäßig NICHT eingerichtet.
- `references/dns-provider-api.md` — exakte, getestete API-Aufrufe für IONOS
  (curl-Beispiele, Record-Formate, Lösch-/Idempotenz-Logik).

Lies die jeweilige reference VOLLSTÄNDIG, bevor du die Phase ausführst — sie enthält
die hart erarbeiteten Details, die zwischen "läuft" und "scheitert" entscheiden.

> **v3-Änderung:** Die öffentliche Dashboard-Subdomain samt Auth-Proxy, systemd-Timer
> und GATE-Passwort wurde entfernt. Die WebUI ist die Oberfläche; das offizielle
> Dashboard nur noch als optionaler SSH-Tunnel (Teil 2, Abschnitt 7). Die
> Passwort-Verifikation (Abschnitt 7.0 in Teil 1) bleibt Pflicht — jetzt nur noch für
> Coolify-Admin und Hermes-WebUI.
