# Changelog — rechnungen-organisieren

## v1.1.0 — 2026-07-29
- Standard-Ordnerstruktur ergänzt (Harald-Feedback): pro Jahr ein Ordner mit `Unsortiert/` und `Bearbeitet/`, damit der Nutzer immer sieht, was schon erledigt ist.
- Übersichtstabelle von CSV auf eine zentrale, dauerhaft aktualisierte `Rechnungsuebersicht.xlsx` umgestellt (Spalten: Jahr, Rechnungsdatum, Rechnungssteller, Original-Dateiname, Neuer Dateiname, Betrag, Ordnerpfad). Wird bei jedem Lauf ergänzt statt überschrieben.
- Anbieter-/Kategorie-/Steuerkategorie-Sortierung ist jetzt optional und sitzt innerhalb von `Bearbeitet/`, statt die einzige Struktur zu sein.

## v1.0.0 — 2026-07-29
- Ersterstellung: deutsche Adaption des „Invoice Organizer" von ComposioHQ (Apache-2.0). Übersetzung, deutsche Rechnungsfelder, Datenschutz-Hinweis, Aufbewahrungshinweis (§ 14b UStG).
