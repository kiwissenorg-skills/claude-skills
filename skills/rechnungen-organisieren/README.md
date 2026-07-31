# Rechnungen organisieren

> Version 1.2.1 · Stand 31.07.2026 · Community · ein Skill von KI-Wissen.org

## Was dieser Skill für dich tut

Räumt einen unordentlichen Ordner voller Rechnungen und Belege auf: erkennt Anbieter, Rechnungsnummer, Datum und Betrag, legt für jede Rechnung eine einheitlich benannte Kopie in sauberen Jahresordnern ab — und pflegt dabei eine zentrale Excel-Übersicht für deine Buchhaltung oder deinen Steuerberater. Die Originaldatei bleibt dabei immer unverändert erhalten.

## Wann der Skill reagiert

Der Skill löst aus, wenn du z.B. schreibst:
- „Organisiere meine Rechnungen im Ordner Rechnungen 2026."
- „Räum meinen Rechnungsordner auf."
- „Sortiere meine Belege für die Buchhaltung."
- „Bereite meine Rechnungen für den Steuerberater vor."

Er reagiert **nicht** bei neuen Angeboten/Rechnungen, die du selbst schreiben willst, und nicht bei Steuerberatung oder Buchungssätzen.

## Installation

1. `SKILL.md` aus diesem Ordner herunterladen.
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Fertig — du prüfst es, indem du Claude bittest: „Organisiere die Rechnungen in [Ordner]." Reagiert Claude mit einer Nachfrage zur Sortierung, läuft der Skill.

## Anwendungsbeispiele

**Beispiel 1**
Du: „Organisiere die Rechnungen in meinem Ordner ~/Dokumente/Rechnungen."
Ergebnis: Claude liest jede Datei aus, fragt kurz, ob zusätzlich nach Anbieter/Kategorie sortiert werden soll, legt danach pro Jahr `Originalrechnungen/` und `Rechnungen sortiert/` an und aktualisiert die zentrale `Rechnungsuebersicht.xlsx`.

**Beispiel 2**
Du: „Räum meinen Rechnungsordner auf, sortiere zusätzlich nach Anbieter."
Ergebnis: Innerhalb von `Rechnungen sortiert/` entstehen zusätzlich Unterordner wie `Telekom/` oder `Amazon/`; `Originalrechnungen/` bleibt unstrukturiert, damit Originale schnell auffindbar bleiben.

## Voraussetzungen

Zugriff auf den Rechnungsordner — lokal über Claude Desktop/Cowork mit Ordnerzugriff, oder per Datei-Upload im Chat. Für die Excel-Übersicht ist keine zusätzliche Software nötig, Claude erstellt und aktualisiert `Rechnungsuebersicht.xlsx` selbst.

## Was ist neu in dieser Version

**v1.2.1:** Nur Dokumentation überarbeitet — Branding-Footer in der SKILL.md ergänzt, README vollständig nach dem KI-Wissen.org-Standard neu aufgebaut (Trigger-Beispiele, Anwendungsbeispiele, Voraussetzungen, Troubleshooting, Support-Zeile). Am Verhalten des Skills ändert sich nichts.

Ältere Änderungen (Original-Erhalt, Excel-Übersicht, Ordnerstruktur) siehe [CHANGELOG.md](CHANGELOG.md).

## Wenn etwas nicht klappt

- Skill reagiert nicht? → Formuliere die Anfrage mit einem der Beispielsätze oben, z.B. „Organisiere meine Rechnungen im Ordner …".
- Ergebnis unvollständig oder Angaben fehlen? → Der Skill markiert solche Fälle in der Zusammenfassung als „manuell prüfen", statt zu raten — dort nachschauen.
- Sehr viele Dateien (mehrere hundert)? → Der Skill arbeitet automatisch in Gruppen von ca. 20–30 Dateien mit Zwischenstand ab.
- Weitere Fragen? → Kontakt unten.

## Herkunft & Lizenz

Basiert auf dem englischsprachigen ["Invoice Organizer"](https://github.com/ComposioHQ/awesome-claude-skills/blob/master/invoice-organizer/SKILL.md) von ComposioHQ (Apache License 2.0), übersetzt und an deutsche Rechnungsangaben, Buchhaltungspraxis und Aufbewahrungspflichten (§ 14b UStG) angepasst.

Dieses Projekt steht ebenfalls unter der **Apache License 2.0** (siehe `LICENSE`). Änderungen gegenüber dem Original: vollständige Übersetzung ins Deutsche, deutsche Rechnungsfeld-Erkennung, deutsche Aufbewahrungshinweise, Datenschutz-Hinweis, angepasste Fehlerbehandlung für große Ordner.

## Wichtiger Hinweis

Dieser Skill ersetzt keine Steuerberatung. Er organisiert Belege, prüft aber keine steuerliche Korrektheit. Bei rechtlichen oder steuerlichen Fragen bitte mit einem Steuerberater abstimmen.

---
Fragen oder Probleme? → https://ki-wissen.org · Ein Skill von KI-Wissen.org (Harald Frey)
