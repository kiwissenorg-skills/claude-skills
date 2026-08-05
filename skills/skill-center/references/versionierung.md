# Versionierung

Schema: **MAJOR.MINOR.PATCH** (Semver). Start bei **v1.0** (= 1.0.0).

## Wann welche Stelle erhöhen
- **PATCH** (1.2.0 → 1.2.1): kleine Korrekturen, Tippfehler, Trigger leicht nachgeschärft, kein Verhaltenswechsel für den Kunden.
- **MINOR** (1.2.1 → 1.3.0): neue Fähigkeit ergänzt, neues Beispiel/Outputvariante, abwärtskompatibel — Kunde kann alles wie bisher nutzen.
- **MAJOR** (1.3.0 → 2.0.0): grundlegender Umbau, geändertes Outputformat oder geänderte Bedienung — der Kunde muss evtl. umlernen.

## Regeln
1. **Vor jeder Änderung** die aktuelle Version nach `Archiv/<skill-name>/v<alt>/` kopieren. Archiv ist eingefroren, wird nie überschrieben.
2. Jede neue Version bekommt einen `CHANGELOG.md`-Eintrag: Version, Datum, Änderung in einem Satz.
3. Nach jeder Versionserhöhung Status auf **„in Arbeit"** → muss neu getestet werden, bevor wieder „freigegeben".
4. Versionsnummer steht im Frontmatter-Kommentar des Skills, im CHANGELOG, im REGISTER und im Dateinamen des ausgelieferten Pakets.

## CHANGELOG-Format
```
# Changelog — <skill-name>

## v1.3.0 — 2026-06-02
- Trigger um Phrasen "X", "Y" erweitert
- Beispielblock für Standardfall ergänzt

## v1.0.0 — 2026-05-20
- Ersterstellung
```
