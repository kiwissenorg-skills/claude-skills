# Changelog — rechnungen-organisieren

## v1.2.0 — 2026-07-30
- Originaldateien bleiben jetzt grundsätzlich erhalten (Harald-Feedback): der Skill benennt nur noch eine Kopie um, das Original wandert unverändert in einen neuen `Originalrechnungen/`-Ordner je Jahr.
- `Bearbeitet/` in `Rechnungen sortiert/` umbenannt — dort landen ausschließlich die umbenannten Kopien.
- Excel-Übersicht um eine zweite Pfadspalte erweitert: **Pfad Original** und **Pfad sortiert** statt einer einzigen `Ordnerpfad`-Spalte, damit beide Ablageorte pro Rechnung nachvollziehbar sind.

## v1.1.0 — 2026-07-29
- Standard-Ordnerstruktur ergänzt (Harald-Feedback): pro Jahr ein Ordner mit `Unsortiert/` und `Bearbeitet/`, damit der Nutzer immer sieht, was schon erledigt ist.
- Übersichtstabelle von CSV auf eine zentrale, dauerhaft aktualisierte `Rechnungsuebersicht.xlsx` umgestellt (Spalten: Jahr, Rechnungsdatum, Rechnungssteller, Original-Dateiname, Neuer Dateiname, Betrag, Ordnerpfad). Wird bei jedem Lauf ergänzt statt überschrieben.
- Anbieter-/Kategorie-/Steuerkategorie-Sortierung ist jetzt optional und sitzt innerhalb von `Bearbeitet/`, statt die einzige Struktur zu sein.

## v1.0.0 — 2026-07-29
- Ersterstellung: deutsche Adaption des „Invoice Organizer" von ComposioHQ (Apache-2.0). Übersetzung, deutsche Rechnungsfelder, Datenschutz-Hinweis, Aufbewahrungshinweis (§ 14b UStG).
