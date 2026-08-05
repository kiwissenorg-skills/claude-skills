# Coolify + Hermes Deployer (Hetzner)

> Community · ein Skill von KI-Wissen.org

## Was dieser Skill für dich tut

Richtet auf einem Hetzner-Server vollautomatisch [Coolify](https://coolify.io) und den Hermes-Agenten (Agent + WebUI) ein und verbindet auf Wunsch Subdomains über die IONOS-DNS-API — inklusive automatischem Let's-Encrypt-SSL über Coolify. Der Skill arbeitet in zwei Phasen (Server/Coolify/Hermes, dann Subdomains/SSL), die jeweils mit einem eingebauten Selbst-Test samt automatischer Reparatur abschließen, bevor es weitergeht. Es entstehen bewusst nur zwei öffentliche Oberflächen — `coolify.<domain>` und `hermes.<domain>` — kein zusätzliches, öffentlich erreichbares Dashboard.

## Wann der Skill reagiert

Der Skill löst aus, wenn du z. B. schreibst:
- „Richte mir Coolify ein."
- „Installier Hermes auf einem Server."
- „Ich will einen eigenen Agenten hosten."
- „Verbinde eine Subdomain mit meinem Server."
- „Hetzner-Server mit Coolify aufsetzen."

## Installation

1. `SKILL.md` aus diesem Ordner herunterladen (inkl. Unterordner `references/`, wird für die eigentliche Ausführung benötigt).
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Los — beim Start fragt der Skill, was du brauchst (Server+Coolify+Hermes neu aufsetzen, oder nur Subdomains an einen bestehenden Server anbinden) und welche Zugangsdaten vorliegen.

## Voraussetzungen

- Ein Hetzner-Cloud-Konto mit API-Token (Lese- und Schreibrechte) für die Servereinrichtung.
- Für Subdomains zusätzlich: eine Domain plus IONOS-DNS-API-Zugangsdaten.
- Bereitschaft, die Server-Erstellung ausdrücklich zu bestätigen — der Skill legt nie eigenständig einen Server an.

## Wenn etwas nicht klappt

- Selbst-Test schlägt fehl? → Der Skill repariert bekannte Fehlerquellen automatisch und testet erneut; ohne grünen Test geht es nicht in die nächste Phase.
- Passwort wird nicht direkt genannt? → Absicht: Jedes Passwort wird erst frisch gegen den laufenden Server verifiziert, bevor es ausgegeben wird.
- Kein öffentliches Hermes-Dashboard vorhanden? → Bewusste Design-Entscheidung (Sicherheit); der offizielle Weg dorthin läuft optional über einen SSH-Tunnel, siehe `references/teil2-subdomains-ssl.md`.

## Herkunft & Lizenz

Eigenentwicklung von KI-Wissen.org (Harald Frey). Dieses Projekt steht unter der **Apache License 2.0** (siehe `LICENSE`).

---
Fragen oder Probleme? → https://ki-wissen.org · Ein Skill von KI-Wissen.org (Harald Frey)
