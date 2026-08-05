# Auslieferung

Nur Skills mit Status **freigegeben ✅** dürfen verpackt werden.

## Format wählen
- **`.skill`** — ein einzelner Skill. Inhalt: ZIP des Skill-Ordners mit `SKILL.md`, `README.md`, `CHANGELOG.md`, ggf. `references/`. (Keine `evals/` mitliefern — das sind interne Testdaten.) Für Kunden, die genau einen Skill installieren.
- **`.plugin`** — mehrere Skills gebündelt. Enthält `.claude-plugin/plugin.json`, mehrere `skills/<name>/SKILL.md`, eine Paket-`README.md`. Für Kunden, die ein ganzes Paket / einen Marketplace bekommen.

Im Zweifel Harald fragen, welches Format der Kunde braucht.

## Paket bauen — Schritte
1. Status prüfen (REGISTER). Nicht freigegeben → abbrechen.
2. README.md auf aktuellen Stand prüfen.
3. Kopie des Skill-Ordners OHNE `evals/` erstellen.
4. ZIP packen und mit korrekter Endung benennen:
   - `Auslieferung/<skill-name>-v<version>.skill`
   - oder `Auslieferung/<paketname>-v<version>.plugin`
5. Datei mit `present_files` zeigen.
6. REGISTER aktualisieren (ausgeliefert am, an Kunde, Version).

## plugin.json (nur bei .plugin)
```json
{
  "name": "<paketname>",
  "version": "<x.y.z>",
  "description": "<kurze Beschreibung des Pakets>",
  "author": { "name": "Harald Frey" }
}
```
Name in kebab-case. Version = Paketversion (kann von Einzelskill-Versionen abweichen).

## Hinweis zu Kundenanpassung
Soll das Paket an viele fremde Kunden gehen und tool-unabhängig sein, statt fester Produktnamen `~~kategorie`-Platzhalter verwenden (z.B. `~~projekt-tracker`) und eine `CONNECTORS.md` beilegen, die erklärt, dass der Kunde dort sein eigenes Tool einsetzt.
