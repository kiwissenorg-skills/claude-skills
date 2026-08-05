# Feedback-Protokoll — <skill-name>

Beobachtungen aus echter Nutzung. Jeder Eintrag wird beim nächsten Audit (Befehl 1)
automatisch berücksichtigt. Behobene Einträge nie löschen — Status auf „behoben" setzen,
damit die Historie erhalten bleibt.

## Eintrag-Format

```
## 2026-06-04 — Status: offen
**Was passiert ist:** Skill „angebot-erstellen" hat bei „schreib eine Rechnung an X" ausgelöst.
**Erwartet:** Kein Triggern — Rechnungen sind explizit ausgeschlossen.
**Einordnung:** description-Problem (Über-Triggern) | Verhaltens-Problem | UX-Problem
**Vorgeschlagener Fix:** Negativ-Abgrenzung in der description schärfen: „NICHT bei Rechnungen …"
**Neuer Testfall:** ja → evals.json #4 („soll NICHT triggern"-Fall)
```

Nach Behebung:

```
## 2026-06-04 — Status: behoben in v1.2.1
...
```

## Regeln

1. Jeder gemeldete Fehlgriff wird **sofort** hier eingetragen — auch wenn der Fix später kommt.
2. Aus jedem Fehlgriff wird ein **neuer Testfall** in `evals.json`, damit derselbe Fehler nie
   wieder unbemerkt passiert (Regression-Schutz).
3. Einordnung immer in eine der drei Kategorien: description (Triggern),
   Verhalten (Skill-Inhalt), UX (was der Nutzer sieht/klickt).
4. Nichts ohne Haralds OK am Skill ändern — Feedback erfassen ja, Fix erst nach Freigabe.
