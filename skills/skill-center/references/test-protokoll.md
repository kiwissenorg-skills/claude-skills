# Test-Protokoll

So wird ein Skill automatisch getestet und der Testbericht erzeugt.

## Bewertungsregeln pro Testfall
Für jeden Testfall prüft der Test-Subagent drei Dinge:
1. **Triggert** — Würde der Skill bei dieser Eingabe auslösen? (Bei „soll NICHT triggern"-Fällen umgekehrt.)
   **Wichtig: 3 Durchläufe pro Trigger-Test.** Triggern ist nicht deterministisch — jeden Trigger-Fall dreimal unabhängig simulieren und die Quote notieren (3/3, 2/3, 1/3). Bestanden nur bei 3/3. 2/3 = wackelig → description schärfen.
2. **Inhalt** — Enthält das erzeugte Ergebnis die im Testfall geforderten Bestandteile (`expect_contains`)?
3. **Format** — Stimmt das Outputformat (z.B. Tabelle, docx, Abschnittsstruktur), falls gefordert?

Ergebnis je Testfall: **bestanden** oder **durchgefallen** + ein Satz Begründung + Trigger-Quote.

## Modell-Vorgabe
- **Entwickeln** (Audit, Überarbeiten, Neu bauen, Doku): stärkstes verfügbares Modell (Opus) — Konzeptarbeit, kleines Volumen.
- **Test-Subagenten: immer mit `model: sonnet` starten.** Sonnet ist die Freigabe-Referenz, weil die meisten KI-Wissen-User damit arbeiten. Ein Skill, der nur mit Opus funktioniert, ist nicht freigabefähig.
- Das im Testbericht/REGISTER vermerkte Modell ist das **Test-Modell des Subagenten** (z.B. „Sonnet 4.6"), nicht das Modell des Hauptchats.
- Hinweis: Der Subagent simuliert das Triggern anhand der description — eine gute Näherung, kein 1:1-Ersatz für einen echten Nutzer-Chat. Stichproben in einer echten Session mit installiertem Skill bleiben sinnvoll.

## Subagent-Auftrag (Vorlage)
Dem `general-purpose`-Subagenten übergeben (mit `model: sonnet`):
- Den vollständigen SKILL.md-Inhalt.
- Die Testfälle aus `evals.json`.
- Diese Bewertungsregeln.
- Auftrag: „Simuliere für jeden Testfall, ob und wie der Skill reagiert. Bewerte bestanden/durchgefallen pro Kriterium. Gib eine kompakte Tabelle + Begründungen zurück. Nenne konkret, was bei Fehlschlägen fehlt."

Bei mehreren unabhängigen Skills: mehrere Subagenten in einem Rutsch parallel starten.

## Testbericht — feste Struktur
Speichern als `evals/testbericht-v<version>-<datum>.md`:

```
# Testbericht — <skill-name> v<version>
Datum: <datum>   |   Modell: <modellname>   |   Getestete Fälle: <n>   |   Bestanden: <x>/<n>

## Ergebnis: <FREIGEGEBEN ✅ | IN ARBEIT ⚠️>

## Einzelergebnisse
| # | Testfall | Trigger-Quote | Inhalt | Format | Urteil |
|---|----------|---------------|--------|--------|--------|
| 1 | ...      | 3/3           | ✅     | ✅     | bestanden |

## Gefundene Mängel (falls vorhanden)
- ...

## Empfohlene Fixes
- ...

## Automatisch geprüft / NICHT geprüft
Geprüft: Triggern, Inhaltselemente, Format.
Nicht automatisch prüfbar: subjektive Qualität (Tonfall, Geschmack) — ein finaler menschlicher Blick empfohlen.
```

## Freigabe-Logik (strikt)
- Alle Fälle bestanden → **FREIGEGEBEN ✅**, Skill darf ausgeliefert werden.
- Mindestens ein Fall durchgefallen → **IN ARBEIT ⚠️**, Mängel + Fixes ausgeben, Auslieferung gesperrt.
