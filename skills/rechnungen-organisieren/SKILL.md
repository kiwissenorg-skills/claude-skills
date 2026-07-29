---
name: rechnungen-organisieren
description: Sortiert und benennt eingehende Rechnungen und Belege automatisch für die deutsche Buchhaltung — liest unordentliche Rechnungsordner aus, erkennt Anbieter, Rechnungsnummer, Datum und Betrag, benennt die Dateien einheitlich und sortiert sie in saubere Ordner. Nutze diesen Skill IMMER, wenn jemand Rechnungen automatisch benennen, einsortieren, aufräumen oder für die Buchhaltung/Steuerberater vorbereiten möchte. Trigger-Begriffe: "Rechnungen sortieren", "Rechnungen automatisch benennen", "Rechnungsordner aufräumen", "Belege einsortieren", "Rechnungen für die Buchhaltung vorbereiten", "organisiere meine Rechnungen", "räum meinen Rechnungsordner auf". NICHT triggern bei: Angebots- oder Rechnungserstellung (das Schreiben neuer Rechnungen), Steuerberatung oder Buchungssätzen.
license: Apache-2.0
---

# Rechnungen organisieren

Dieser Skill räumt einen unordentlichen Ordner voller Rechnungen und Belege auf: einheitlich benannt, sinnvoll einsortiert, mit einer Übersichtstabelle für die Buchhaltung oder den Steuerberater.

Basiert auf dem englischsprachigen "Invoice Organizer" von [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills/blob/master/invoice-organizer/SKILL.md) (Apache-2.0-Lizenz), übersetzt und an deutsche Rechnungsangaben, Buchhaltungspraxis und Aufbewahrungspflichten angepasst — erstellt für [ki-wissen.org](https://ki-wissen.org).

## Wichtiger Hinweis

Dieser Skill ersetzt keine Steuerberatung. Er organisiert Belege, prüft aber keine steuerliche Korrektheit. Bei rechtlichen oder steuerlichen Fragen bitte mit einem Steuerberater abstimmen.

## Ordnerstruktur (Standard)

Damit der Nutzer jederzeit den Überblick behält, legt der Skill standardmäßig diese Struktur an — pro Jahr ein Ordner mit klarer Trennung zwischen unbearbeitet und fertig:

```
Rechnungen/
  Rechnungsuebersicht.xlsx      ← EINE zentrale Übersicht, wird bei jedem Lauf aktualisiert
  2026/
    Unsortiert/                 ← neue, noch nicht bearbeitete Rechnungen landen hier
    Bearbeitet/                 ← fertig benannte, einsortierte Rechnungen
      Telekom/                  ← optional: zusätzlich nach Anbieter/Kategorie, wenn gewünscht (siehe unten)
  2025/
    Bearbeitet/
```

Diese Jahr/Unsortiert/Bearbeitet-Struktur ist der Standard und wird ohne Rückfrage angelegt. Eine zusätzliche Unterteilung innerhalb von `Bearbeitet/` (nach Anbieter, Kategorie, Steuerkategorie) ist optional — das fragt der Skill in Schritt 3 ab.

## Ablauf

1. **Ordner scannen** — alle PDF-, JPG- und PNG-Dateien im angegebenen Ordner identifizieren (auch E-Mail-Anhänge und Screenshots von Rechnungen). Liegt schon eine Jahr/Unsortiert-Struktur vor, dort scannen; sonst den vom Nutzer genannten Ordner als "Unsortiert" behandeln.
2. **Informationen auslesen** — aus jeder Datei werden erkannt:
   - Anbieter/Aussteller (Firmenname)
   - Rechnungsnummer
   - Rechnungsdatum
   - Gesamtbetrag (brutto)
   - Leistungsbeschreibung (kurz, z. B. "Software-Abo", "Büromaterial")
   Gescannte Belege und Fotos werden über Claudes Bilderkennung gelesen — keine zusätzliche OCR-Software nötig.
3. **Vorgehen abstimmen** — bevor irgendetwas verschoben wird, mit dem Nutzer klären, ob innerhalb von `Bearbeitet/` zusätzlich nach Anbieter, Kategorie oder Steuerkategorie unterteilt werden soll, oder ob alles direkt in `Bearbeitet/` liegen soll (siehe Sortiermuster unten).
4. **Einheitlich benennen** — Format: `JJJJ-MM-TT Anbieter - Rechnung - Leistung.pdf`, Beispiel: `2026-03-15 Telekom - Rechnung - Internet-Abo.pdf`. Das Datum vorne sorgt dafür, dass Dateien in jedem Ordner automatisch chronologisch sortiert sind.
5. **Jahresordner anlegen und Dateien verschieben** — NUR nach ausdrücklicher Bestätigung durch den Nutzer. Jede Datei wandert in den zum Rechnungsdatum passenden Jahresordner nach `Bearbeitet/` (ggf. weiter unterteilt laut Schritt 3). Originaldateien werden dabei nicht gelöscht, sondern verschoben.
6. **Zentrale Excel-Übersicht aktualisieren** — `Rechnungsuebersicht.xlsx` im Wurzelordner. Existiert sie schon, werden neue Zeilen ergänzt (keine Dubletten anlegen); existiert sie nicht, wird sie neu erstellt. Spalten: **Jahr, Rechnungsdatum, Rechnungssteller, Original-Dateiname, Neuer Dateiname, Betrag, Ordnerpfad**. Diese eine Tabelle gibt dem Nutzer jederzeit die Gesamtübersicht über alle Jahre hinweg — direkt verwendbar für die eigene Buchhaltung oder zur Weitergabe an den Steuerberater.
7. **Zusammenfassung geben** — Anzahl verarbeiteter Dateien, Zeitraum, Gesamtsumme, und Hinweis auf alles, was manuell geprüft werden sollte.

## Sortiermuster innerhalb von „Bearbeitet/" (optional, zur Auswahl anbieten)

- **Keine weitere Unterteilung:** alles direkt in `Bearbeitet/`
- **Nach Anbieter:** `Bearbeitet/Telekom/`, `Bearbeitet/Amazon/`
- **Nach Kategorie:** `Bearbeitet/Software/`, `Bearbeitet/Buero/`, `Bearbeitet/Reisen/`
- **Nach Quartal:** `Bearbeitet/Q1/`
- **Nach Steuerkategorie:** `Bearbeitet/Absetzbar/`, `Bearbeitet/Privat/`

## Sonderfälle

- **Fehlende Angaben:** Datei wird trotzdem verschoben, aber in der Zusammenfassung als "manuell prüfen" markiert — nicht raten.
- **Duplikate:** werden per Dateivergleich erkannt und dem Nutzer gemeldet, bevor sie doppelt einsortiert werden.
- **Mehrseitige Rechnungen:** zusammengehörige Seiten werden nach Möglichkeit zu einer Datei zusammengeführt.
- **Sehr große Ordner (mehrere hundert Dateien):** in Gruppen von ca. 20–30 Dateien abarbeiten und nach jeder Gruppe kurz Zwischenstand geben, statt alles auf einmal zu verarbeiten.

## Datenschutz

Rechnungen enthalten sensible Finanzdaten. Läuft der Skill lokal (z. B. über Claude Desktop/Cowork mit direktem Zugriff auf den eigenen Rechner), verlassen die Dateien den eigenen Rechner nicht. Bei Nutzung über eine Cloud-Umgebung gilt das nicht automatisch — im Zweifel vorher prüfen, wo die Dateien verarbeitet werden.

## Aufbewahrung (Hinweis, keine Rechtsberatung)

In Deutschland müssen Rechnungen in der Regel 10 Jahre aufbewahrt werden (§ 14b UStG). Dieser Skill organisiert die Belege, ersetzt aber keine rechtssichere Archivierung — bei Unsicherheit den Steuerberater fragen.
