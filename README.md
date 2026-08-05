# Claude Skills von KI-Wissen.org

[![Lizenz: Apache 2.0](https://img.shields.io/badge/Lizenz-Apache%202.0-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/kiwissenorg-skills/claude-skills?style=social)](https://github.com/kiwissenorg-skills/claude-skills/stargazers)
![Sprache: Deutsch](https://img.shields.io/badge/Sprache-Deutsch-black)

Fertige, deutschsprachige [Claude Skills](https://www.anthropic.com/news/skills) zum kostenlosen Download — praxiserprobt, dokumentiert und mit passender Video-Anleitung auf [KI-Wissen.org](https://ki-wissen.org).

Diese Sammlung wächst laufend. Jeder Skill hier wurde erst selbst im Alltag genutzt, bevor er veröffentlicht wurde.

## Was ist ein Claude Skill?

Ein Skill ist eine Sammlung aus Anleitung (`SKILL.md`) und optionalen Zusatzdateien, die Claude beibringt, eine wiederkehrende Aufgabe zuverlässig und auf eine bestimmte Art zu erledigen — z. B. Rechnungen ordnen, ein Angebot schreiben oder einen Datensatz auf DSGVO prüfen. Einmal installiert, ruft Claude den Skill automatisch auf, sobald die Aufgabe dazu passt.

## Skills

| Skill | Beschreibung | Anleitung |
|---|---|---|
| [hetzner-coolify-hermes](skills/hetzner-coolify-hermes) | Richtet auf einem Hetzner-Server vollautomatisch Coolify und den Hermes-Agenten ein und verbindet optional Subdomains via IONOS-DNS-API inkl. automatischem SSL. | [Video-Anleitung](https://ki-wissen.org/?post_type=ki-anleitungen&p=7664) |
| [morgen-dashboard](skills/morgen-dashboard) | Erstellt ein kompaktes Tages-Dashboard als HTML-Datei mit Kalender, Aufgaben, Inbox, Wetter und News. | [Video-Anleitung](https://ki-wissen.org/ki-anleitungen/morgen/) |
| [prozess-interview](skills/prozess-interview) | Interviewt dich Schritt für Schritt, um eine Idee oder ein Vorhaben sauber zu durchdenken, bevor etwas gebaut wird — Ergebnis ist ein strukturierter Prozess-Steckbrief. | [Video-Anleitung](https://ki-wissen.org/?post_type=ki-anleitungen&p=7784) |
| [rechnungen-organisieren](skills/rechnungen-organisieren) | Räumt einen unordentlichen Rechnungsordner auf: einheitlich benannt, in Jahresordner sortiert, mit zentraler Excel-Übersicht für die Buchhaltung. | [Video-Anleitung](https://ki-wissen.org/ki-anleitungen/rechnungen-organisieren/) |
| [schreibe-in-meinem-stil](skills/schreibe-in-meinem-stil) | Schreibt Texte im persönlichen Schreibstil des Nutzers und entfernt zugleich typische Spuren KI-generierter deutscher Texte. | [Video-Anleitung](https://ki-wissen.org/ki-anleitungen/skill/) |
| [skill-center](skills/skill-center) | Kommandozentrale für professionelle Skill-Entwicklung: Auswerten, Überarbeiten, Testen, Dokumentieren, Versionieren und Ausliefern von Skills. | – |
| [verblenden-skill](skills/verblenden-skill) | Anonymisiert (verblendet) personenbezogene Daten in Dokumenten und stellt sie bei Bedarf wieder her (entblendet) — Mapping bleibt lokal. | [Video-Anleitung](https://ki-wissen.org/ki-anleitungen/persoenliche-daten-automatisch/) |

## Installation

1. Ordner des gewünschten Skills öffnen (z. B. [`skills/rechnungen-organisieren`](skills/rechnungen-organisieren)) und `SKILL.md` herunterladen (bei Skills mit `references/`-Unterordner diesen ebenfalls mit herunterladen).
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Los — Claude nutzt den Skill automatisch, sobald die passende Aufgabe kommt.

Ausführliche Schritt-für-Schritt-Anleitungen (inkl. Praxisbeispiel) gibt es jeweils als Video unter [ki-wissen.org/anleitungen](https://ki-wissen.org/anleitungen/).

## Herkunft & Lizenz

Jeder Skill-Ordner enthält seine eigene Lizenz und ggf. einen Herkunftshinweis, falls er auf einer bestehenden Vorlage aufbaut (z. B. übersetzt und an deutsche Gegebenheiten angepasst). Das Repository selbst steht unter der [Apache License 2.0](LICENSE).

## Über KI-Wissen.org

[KI-Wissen.org](https://ki-wissen.org) hilft kleinen Betrieben und Selbstständigen ohne IT-Abteilung dabei, KI im Alltag sinnvoll einzusetzen — mit kostenlosen Anleitungen, einem YouTube-Kanal und einem Marktplatz für geprüfte KI-Fachleute. Fragen oder Wünsche zu weiteren Skills? Einfach ein [Issue](../../issues) aufmachen oder den [Newsletter „KI-Kompass"](https://ki-wissen.org/newsletter/) abonnieren.

## Mitmachen

Fehler gefunden, ein Skill funktioniert nicht wie beschrieben, oder du wünschst dir einen neuen Skill? Siehe [CONTRIBUTING.md](CONTRIBUTING.md). Für den Umgang miteinander gilt unser [Code of Conduct](CODE_OF_CONDUCT.md), Sicherheitsprobleme bitte gemäß [SECURITY.md](SECURITY.md) melden.

## Haftungsausschluss & Rechtliche Hinweise / Disclaimer

### Inoffizielles Projekt

Dies ist ein inoffizielles Community-Projekt von KI-Wissen.org. Es steht in keiner Verbindung zu Anthropic PBC, wird von Anthropic weder unterstützt noch gesponsert. „Claude" und „Model Context Protocol" sind Marken von Anthropic.

### Haftungsausschluss (Disclaimer)

Die Nutzung dieser Skills erfolgt auf eigene Verantwortung. Sie werden „wie besehen" (as is) ohne jegliche Gewährleistung für Funktionalität, Vollständigkeit oder Richtigkeit bereitgestellt. Der Autor haftet nicht für Schäden, Datenverluste oder sonstige Folgen, die aus der Nutzung entstehen.

---

### Disclaimer (English)

This is an unofficial community project by KI-Wissen.org and is not affiliated with, endorsed by, or sponsored by Anthropic PBC. Use these skills at your own risk. Provided "AS IS" without warranty of any kind.
