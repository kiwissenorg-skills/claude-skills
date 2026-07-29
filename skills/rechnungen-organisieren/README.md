# Rechnungen organisieren — ein Claude Skill

Automatisiert das Aufräumen von Rechnungsordnern: liest eingehende Rechnungen und Belege aus, benennt sie einheitlich (`JJJJ-MM-TT Anbieter - Rechnung - Leistung.pdf`) und sortiert sie in Jahresordner mit klarer Trennung zwischen `Unsortiert/` und `Bearbeitet/` — inklusive einer zentralen, dauerhaft aktualisierten Excel-Übersicht (`Rechnungsuebersicht.xlsx`) für die Buchhaltung.

Ein kostenloser Skill von [KI-Wissen.org](https://ki-wissen.org) — Teil der Reihe "Buchhaltung mit Claude automatisieren". Die dazugehörige Video-Anleitung (Schritt-für-Schritt-Einrichtung und Praxisbeispiel) findest du unter [ki-wissen.org/anleitungen/buchhaltung](https://ki-wissen.org/anleitungen/buchhaltung/).

## Installation

1. `SKILL.md` herunterladen.
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Claude bitten: "Organisiere die Rechnungen in [Ordner]."

## Herkunft & Lizenz

Basiert auf dem englischsprachigen ["Invoice Organizer"](https://github.com/ComposioHQ/awesome-claude-skills/blob/master/invoice-organizer/SKILL.md) von ComposioHQ (Apache License 2.0), übersetzt und an deutsche Rechnungsangaben, Buchhaltungspraxis und Aufbewahrungspflichten (§ 14b UStG) angepasst.

Dieses Projekt steht ebenfalls unter der **Apache License 2.0** (siehe `LICENSE`). Änderungen gegenüber dem Original: vollständige Übersetzung ins Deutsche, deutsche Rechnungsfeld-Erkennung, deutsche Aufbewahrungshinweise, Datenschutz-Hinweis, angepasste Fehlerbehandlung für große Ordner.

## Wichtiger Hinweis

Dieser Skill ersetzt keine Steuerberatung. Er organisiert Belege, prüft aber keine steuerliche Korrektheit.
