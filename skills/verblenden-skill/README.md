# Verblenden & Entblenden

> Community · ein Skill von KI-Wissen.org

## Was dieser Skill für dich tut

Ein Datenschutz-Skill mit zwei Modi: **Verblenden** (Anonymisieren) und **Entblenden** (Re-Identifizieren). Verblenden ersetzt alle personenbezogenen und datenschutzrelevanten Angaben in einem Dokument durch neutrale Platzhalter-IDs (z. B. `PERSON_01`, `FIRMA_01`), speichert ein Mapping als CSV und legt das anonymisierte Dokument ab. Entblenden liest das Mapping und stellt das Original wieder her. Die echten Daten verlassen dabei nie den eigenen Rechner — die Mapping-Tabelle bleibt immer lokal.

## Wann der Skill reagiert

Der Skill löst aus, wenn du z. B. schreibst:
- „Verblende das Dokument" / „anonymisiere den Text."
- „Entblende die Datei" / „stell das Original wieder her."
- „Mach die Daten unkenntlich" / „ersetze Namen und Adressen."
- Oder bei Begriffen wie Pseudonymisierung, DSGVO-Anonymisierung, PII entfernen, Testdaten anonymisieren.

## Installation

1. `SKILL.md` aus diesem Ordner herunterladen.
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Los — der Skill fragt zu Beginn, ob verblendet oder entblendet werden soll und wie das Projekt heißt, und legt bei Bedarf automatisch die passende Ordnerstruktur an.

## Anwendungsbeispiele

**Beispiel 1 — Verblenden**
Du legst ein Dokument in `verblenden-skill/[Projekt]/01_eingang/` und sagst: „Verblende das."
Ergebnis: Der Skill erkennt Personen, Firmen, Adressen, Telefonnummern u. a., legt eine Mapping-CSV in `02_mapping/` an und speichert das anonymisierte Dokument in `03_verblendet/` — das Original bleibt unverändert.

**Beispiel 2 — Entblenden**
Du legst ein bearbeitetes, verblendetes Dokument vor und sagst: „Entblende das wieder."
Ergebnis: Der Skill lädt die passende Mapping-CSV, ersetzt alle IDs durch die Originalwerte und speichert das Ergebnis in `05_entblendet/`.

## Voraussetzungen

Lokaler Ordnerzugriff (Claude Desktop/Cowork mit verbundenem Ordner) für die feste Projektstruktur (`01_eingang` bis `05_entblendet`). Für `.docx`-Dateien installiert der Skill bei Bedarf automatisch `python-docx`.

## Wenn etwas nicht klappt

- Keine Dateien in `01_eingang/`? → Der Skill weist darauf hin und wartet, statt zu raten.
- Mehrere Mapping-CSVs vorhanden? → Der Skill fragt nach, welche zum zu entblendenden Dokument passt.
- Noch IDs im entblendeten Ergebnis übrig? → Der Skill prüft das automatisch und weist darauf hin — meist stammen sie aus zusätzlichem, KI-verarbeitetem Text.

## Herkunft & Lizenz

Eigenentwicklung von KI-Wissen.org (Harald Frey). Dieses Projekt steht unter der **Apache License 2.0** (siehe `LICENSE`).

---
Fragen oder Probleme? → https://ki-wissen.org · Ein Skill von KI-Wissen.org (Harald Frey)
