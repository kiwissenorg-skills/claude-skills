---
name: rechnungen-organisieren
description: Sortiert und benennt eingehende Rechnungen und Belege automatisch für die deutsche Buchhaltung — liest unordentliche Rechnungsordner aus, erkennt Anbieter, Rechnungsnummer, Datum und Betrag, benennt eine Kopie einheitlich und sortiert sie in saubere Ordner, während die Originaldatei unverändert erhalten bleibt. Nutze diesen Skill IMMER, wenn jemand Rechnungen automatisch benennen, einsortieren, aufräumen oder für die Buchhaltung/Steuerberater vorbereiten möchte. Trigger-Begriffe: "Rechnungen sortieren", "Rechnungen automatisch benennen", "Rechnungsordner aufräumen", "Belege einsortieren", "Rechnungen für die Buchhaltung vorbereiten", "organisiere meine Rechnungen", "räum meinen Rechnungsordner auf". NICHT triggern bei: Angebots- oder Rechnungserstellung (das Schreiben neuer Rechnungen), Steuerberatung oder Buchungssätzen.
license: Apache-2.0
metadata:
  version: "1.2.1"
  author: "Harald Frey"
---

# Rechnungen organisieren

Dieser Skill räumt einen unordentlichen Ordner voller Rechnungen und Belege auf: einheitlich benannt, sinnvoll einsortiert, mit einer Übersichtstabelle für die Buchhaltung oder den Steuerberater — und ohne dass die Originaldateien verändert oder ersetzt werden.

Basiert auf dem englischsprachigen "Invoice Organizer" von [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills/blob/master/invoice-organizer/SKILL.md) (Apache-2.0-Lizenz), übersetzt und an deutsche Rechnungsangaben, Buchhaltungspraxis und Aufbewahrungspflichten angepasst — erstellt für [ki-wissen.org](https://ki-wissen.org).

## Wichtiger Hinweis

Dieser Skill ersetzt keine Steuerberatung. Er organisiert Belege, prüft aber keine steuerliche Korrektheit. Bei rechtlichen oder steuerlichen Fragen bitte mit einem Steuerberater abstimmen.

## Grundprinzip: Original bleibt immer erhalten

Die Originaldatei wird **nie überschrieben, umbenannt oder gelöscht**. Für jede erkannte Rechnung entstehen zwei Dateien:

1. **Original** — unverändert, mit ursprünglichem Dateinamen, wandert in `Originalrechnungen/`.
2. **Bearbeitete Kopie** — eine Kopie mit einheitlichem, sprechendem Dateinamen, wandert in `Rechnungen sortiert/`.

So bleibt der exakte Originalbeleg (wichtig z. B. bei eingescannten Belegen oder Anhängen) jederzeit auffindbar, während die umbenannte Kopie für den täglichen Gebrauch und die Buchhaltung sorgt.

## Ordnerstruktur (Standard)

Damit der Nutzer jederzeit den Überblick behält, legt der Skill standardmäßig diese Struktur an — pro Jahr ein Ordner mit klarer Trennung zwischen unbearbeitet, Original und bearbeiteter Kopie:

```
Rechnungen/
  Rechnungsuebersicht.xlsx      ← EINE zentrale Übersicht, wird bei jedem Lauf aktualisiert
  2026/
    Unsortiert/                 ← neue, noch nicht bearbeitete Rechnungen landen hier
    Originalrechnungen/         ← unveränderte Originaldateien, Originalname bleibt erhalten
    Rechnungen sortiert/        ← Kopien, einheitlich benannt und einsortiert
      Telekom/                  ← optional: zusätzlich nach Anbieter/Kategorie, wenn gewünscht (siehe unten)
  2025/
    Originalrechnungen/
    Rechnungen sortiert/
```

Diese Jahr/Unsortiert/Originalrechnungen/Rechnungen-sortiert-Struktur ist der Standard und wird ohne Rückfrage angelegt. Eine zusätzliche Unterteilung innerhalb von `Rechnungen sortiert/` (nach Anbieter, Kategorie, Steuerkategorie) ist optional — das fragt der Skill in Schritt 3 ab. `Originalrechnungen/` wird dagegen nie weiter unterteilt, damit die Originale schnell und ohne Rätselraten wiederzufinden sind.

## Ablauf

1. **Ordner scannen** — alle PDF-, JPG- und PNG-Dateien im angegebenen Ordner identifizieren (auch E-Mail-Anhänge und Screenshots von Rechnungen). Liegt schon eine Jahr/Unsortiert-Struktur vor, dort scannen; sonst den vom Nutzer genannten Ordner als "Unsortiert" behandeln.
2. **Informationen auslesen** — aus jeder Datei werden erkannt:
   - Anbieter/Aussteller (Firmenname)
   - Rechnungsnummer
   - Rechnungsdatum
   - Gesamtbetrag (brutto)
   - Leistungsbeschreibung (kurz, z. B. "Software-Abo", "Büromaterial")
   Gescannte Belege und Fotos werden über Claudes Bilderkennung gelesen — keine zusätzliche OCR-Software nötig.
3. **Vorgehen abstimmen** — bevor irgendetwas verschoben wird, mit dem Nutzer klären, ob innerhalb von `Rechnungen sortiert/` zusätzlich nach Anbieter, Kategorie oder Steuerkategorie unterteilt werden soll, oder ob alles direkt in `Rechnungen sortiert/` liegen soll (siehe Sortiermuster unten).
4. **Kopie einheitlich benennen** — von jeder Originaldatei wird eine Kopie erstellt und benannt nach dem Format: `JJJJ-MM-TT Anbieter - Rechnung - Leistung.pdf`, Beispiel: `2026-03-15 Telekom - Rechnung - Internet-Abo.pdf`. Das Datum vorne sorgt dafür, dass Dateien in jedem Ordner automatisch chronologisch sortiert sind. Die Originaldatei behält ihren ursprünglichen Namen.
5. **Jahresordner anlegen, Original und Kopie verschieben** — NUR nach ausdrücklicher Bestätigung durch den Nutzer. Pro Datei landen zwei Dateien im zum Rechnungsdatum passenden Jahresordner:
   - die **Originaldatei** (unverändert, Originalname) → `Originalrechnungen/`
   - die **umbenannte Kopie** → `Rechnungen sortiert/` (ggf. weiter unterteilt laut Schritt 3)
   Die Originaldatei wird dabei verschoben, nicht gelöscht oder überschrieben — sie existiert nach dem Lauf also weiterhin, nur eben in `Originalrechnungen/` statt in `Unsortiert/`.
6. **Zentrale Excel-Übersicht aktualisieren** — `Rechnungsuebersicht.xlsx` im Wurzelordner. Existiert sie schon, werden neue Zeilen ergänzt (keine Dubletten anlegen); existiert sie nicht, wird sie neu erstellt. Spalten: **Jahr, Rechnungsdatum, Rechnungssteller, Original-Dateiname, Neuer Dateiname, Betrag, Pfad Original, Pfad sortiert**. Diese eine Tabelle gibt dem Nutzer jederzeit die Gesamtübersicht über alle Jahre hinweg — direkt verwendbar für die eigene Buchhaltung oder zur Weitergabe an den Steuerberater, und zeigt zu jeder Rechnung sowohl den Ablageort des Originals als auch der sortierten Kopie.
7. **Zusammenfassung geben** — Anzahl verarbeiteter Dateien, Zeitraum, Gesamtsumme, und Hinweis auf alles, was manuell geprüft werden sollte.

## Sortiermuster innerhalb von „Rechnungen sortiert/" (optional, zur Auswahl anbieten)

- **Keine weitere Unterteilung:** alles direkt in `Rechnungen sortiert/`
- **Nach Anbieter:** `Rechnungen sortiert/Telekom/`, `Rechnungen sortiert/Amazon/`
- **Nach Kategorie:** `Rechnungen sortiert/Software/`, `Rechnungen sortiert/Buero/`, `Rechnungen sortiert/Reisen/`
- **Nach Quartal:** `Rechnungen sortiert/Q1/`
- **Nach Steuerkategorie:** `Rechnungen sortiert/Absetzbar/`, `Rechnungen sortiert/Privat/`

`Originalrechnungen/` bleibt in jedem Fall unstrukturiert (keine Unterordner) — dort zählt nur, dass das Original schnell wiederfindbar ist.

## Sonderfälle

- **Fehlende Angaben:** Original und Kopie werden trotzdem verschoben bzw. angelegt, aber in der Zusammenfassung als "manuell prüfen" markiert — nicht raten.
- **Duplikate:** werden per Dateivergleich erkannt und dem Nutzer gemeldet, bevor sie doppelt einsortiert werden.
- **Mehrseitige Rechnungen:** zusammengehörige Seiten werden für die Kopie in `Rechnungen sortiert/` nach Möglichkeit zu einer Datei zusammengeführt; die einzelnen Originalseiten bleiben unverändert in `Originalrechnungen/`.
- **Sehr große Ordner (mehrere hundert Dateien):** in Gruppen von ca. 20–30 Dateien abarbeiten und nach jeder Gruppe kurz Zwischenstand geben, statt alles auf einmal zu verarbeiten.

## Datenschutz

Rechnungen enthalten sensible Finanzdaten. Läuft der Skill lokal (z. B. über Claude Desktop/Cowork mit direktem Zugriff auf den eigenen Rechner), verlassen die Dateien den eigenen Rechner nicht. Bei Nutzung über eine Cloud-Umgebung gilt das nicht automatisch — im Zweifel vorher prüfen, wo die Dateien verarbeitet werden.

## Aufbewahrung (Hinweis, keine Rechtsberatung)

In Deutschland müssen Rechnungen in der Regel 10 Jahre aufbewahrt werden (§ 14b UStG). Da dieser Skill die Originaldatei stets unverändert in `Originalrechnungen/` aufbewahrt, bleibt der ursprüngliche Beleg für die Aufbewahrungsfrist erhalten — der Skill ersetzt aber keine rechtssichere Archivierung; bei Unsicherheit den Steuerberater fragen.

---
*Ein Skill von KI-Wissen.org — Entwickler: Harald Frey · [ki-wissen.org](https://ki-wissen.org)*
