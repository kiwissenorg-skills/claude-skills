---
name: verblenden-skill
description: >
  Datenschutz-Skill mit zwei Modi: **Verblenden** (Anonymisieren) und **Entblenden** (Re-Identifizieren).
  Verblenden ersetzt alle personenbezogenen und datenschutzrelevanten Daten in einem Dokument durch
  neutrale Platzhalter-IDs (z.B. PERSON_01, FIRMA_01), speichert ein Mapping als CSV und legt das
  anonymisierte Dokument ab. Entblenden liest das Mapping und stellt das Original wieder her.
  
  Nutze diesen Skill IMMER wenn Harald oder ein User fragt: „verblende das Dokument", „anonymisiere
  den Text", „entblende die Datei", „mach die Daten unkenntlich", „ersetze Namen und Adressen",
  „re-identifiziere", „stell das Original wieder her", „datenschutzkonform anonymisieren". Auch
  triggern bei Begriffen wie Pseudonymisierung, Anonymisierung, DSGVO-Anonymisierung, Datenschutz-
  Schwärzung, Testdaten anonymisieren, PII entfernen, Namen ersetzen, sensible Daten ersetzen.
  Verwende diesen Skill bei jedem Workflow der Originaldaten anonymisiert an KI-Systeme weitergibt
  und danach die Ergebnisse re-identifiziert.
---

# Verblenden & Entblenden

Dieser Skill schützt personenbezogene Daten durch strukturierte Pseudonymisierung. Dokumente werden
anonymisiert (verblendet), damit sie sicher mit KI-Systemen oder Dritten geteilt werden können —
und danach präzise wiederhergestellt (entblendet).

---

## Start — Immer zuerst

1. Frage den User: **„Verblenden oder Entblenden?"**
2. Frage: **„Wie heißt das Projekt?"**
3. Prüfe ob der Projektordner existiert:

```
verblenden-skill/[Projektname]/
├── 01_eingang/
├── 02_mapping/
├── 03_verblendet/
├── 04_verarbeitet/
└── 05_entblendet/
```

- Existiert der Ordner → weiter mit dem gewählten Modus
- Existiert er nicht → lege ihn mit allen fünf Unterordnern an und bestätige:
  `"Neues Projekt '[Name]' wurde angelegt."` → dann weiter

Der Basispfad ist relativ zum Arbeitsverzeichnis des Users. Verwende beim Anlegen relative Pfade
oder frage nach dem gewünschten Speicherort, falls unklar.

---

## Modus 1: VERBLENDEN

**Eingabe:** Dokument(e) in `verblenden-skill/[Projektname]/01_eingang/`

Falls dort keine Dateien liegen, weise den User darauf hin und warte.

### Schritt 1 — Analysieren

Lies das Dokument vollständig und erkenne alle datenschutzrelevanten Informationen:

| Kategorie | Beispiele |
|-----------|-----------|
| PERSON_ | Vor- und Nachnamen, Initialen, Pseudonyme die Personen identifizieren |
| FIRMA_ | Unternehmens-, Organisations-, Behördenbezeichnungen |
| ADRESSE_ | Straße, PLZ, Ort, Land (wenn einer Person/Firma zuordenbar) |
| TEL_ | Telefon- und Faxnummern |
| EMAIL_ | E-Mail-Adressen |
| NR_ | Vertrags-, Kunden-, Rechnungs-, Patienten-, Konto-, IBAN-Nummern |
| DATUM_ | Geburtsdaten, Behandlungsdaten, Vertragsdaten (wenn personenbezogen) |
| SONSTIGE_ | Alle weiteren identifizierenden Angaben (z.B. Kfz-Kennzeichen, IP-Adressen) |

Zähle alle Fundstellen durch — jeder einmalige Wert bekommt eine eigene ID.
Gleiche Werte bekommen immer dieselbe ID (z.B. erscheint „Max Mustermann" dreimal → immer PERSON_01).

### Schritt 2 — Mapping-Tabelle erstellen

Erstelle eine CSV-Datei in `02_mapping/` mit demselben Dateinamen wie das Original (z.B. `vertrag.txt` → `vertrag.csv`).

Format (Semikolon als Trennzeichen, UTF-8):

```csv
ID;Original
PERSON_01;Max Mustermann
PERSON_02;Anna Schmidt
FIRMA_01;Muster GmbH
ADRESSE_01;Musterstraße 12, 80331 München
TEL_01;+49 89 12345678
EMAIL_01;max@muster.de
NR_001;Vertrag-Nr. 4711
DATUM_01;15.03.1985
```

Die Mapping-Tabelle ist unveränderlich nach Erstellung — sie wird nie überschrieben oder ergänzt.
Sie bleibt immer lokal und verlässt den Rechner nicht.

### Schritt 3 — Verblendetes Dokument erstellen

Erstelle eine Kopie des Originals in `03_verblendet/` mit demselben Dateinamen.
Ersetze alle sensiblen Werte durch die entsprechenden IDs aus dem Mapping.

Das Original in `01_eingang/` bleibt unverändert.

Gib am Ende eine kurze Zusammenfassung aus:
```
✓ Verblendet: [Dateiname]
  Gefundene Einträge: 8 (3 Personen, 2 Firmen, 1 Adresse, 1 Nummer, 1 Datum)
  Mapping gespeichert: 02_mapping/[dateiname].csv
  Verblendetes Dokument: 03_verblendet/[dateiname]
```

**Bei mehreren Dateien in 01_eingang/:** Alle nacheinander verarbeiten, je eine eigene Mapping-CSV.

---

## Modus 2: ENTBLENDEN

**Eingabe:** Dokument in `03_verblendet/` oder `04_verarbeitet/`

Der User legt das zu entblendende Dokument vor. Falls unklar welches, frage nach dem Dateinamen.

### Schritt 1 — Mapping-Tabelle laden

Lade die passende CSV aus `02_mapping/` — der Dateiname entspricht dem Original-Dokumentnamen
(nicht dem verblendeten). Falls mehrere CSVs vorhanden sind, frage den User welche passt.

### Schritt 2 — Entblenden

Lese alle ID→Original-Paare aus der CSV.
Ersetze im Dokument alle IDs durch die Originalwerte (exakte String-Ersetzung, case-sensitiv).

### Schritt 3 — Ergebnis speichern

Speichere das entblendete Dokument in `05_entblendet/` mit demselben Dateinamen.

Gib eine Bestätigung aus:
```
✓ Entblendet: [Dateiname]
  Ersetzt: 12 IDs aus 8 Mapping-Einträgen
  Ergebnis: 05_entblendet/[dateiname]
```

---

## Dateiformat-Regeln

| Format | Vorgehen |
|--------|----------|
| `.txt` | Direkt lesen und bearbeiten |
| `.md` | Direkt lesen und bearbeiten |
| `.docx` | Text mit python-docx extrahieren, verarbeiten, neu als .docx speichern |
| Andere | Nach Möglichkeit als Text behandeln; sonst User fragen |

Für `.docx`-Dateien: Installiere `python-docx` falls nötig (`pip install python-docx --break-system-packages`).
Extrahiere den Text paragraphenweise, ersetze die Werte, schreibe die Paragraphen zurück.
Formatierung (Fett, Kursiv, Schriftgröße) so weit wie möglich erhalten.

---

## Qualitätssicherung

Nach dem Verblenden: Prüfe stichprobenartig, ob noch Originalwerte im verblendeten Dokument
vorkommen, indem du mindestens 2-3 bekannte Namen/Werte suchst.

Nach dem Entblenden: Prüfe, ob noch IDs (Muster: `[A-Z]+_\d+`) im Dokument übrig geblieben sind.
Falls ja, weise den User darauf hin — sie stammen möglicherweise aus dem KI-verarbeiteten Text.
