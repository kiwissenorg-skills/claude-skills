# KI-Wissen.org-Standard

Verbindliche Vorgaben für **jeden** Skill, der über KI-Wissen.org an User geht.
Beim Audit (Befehl 1), beim Neu-bauen (Befehl 3) und vor jeder Auslieferung (Befehl 6) prüfen.
Ein Skill, der diesen Standard nicht erfüllt, ist nicht kundenreif — egal wie gut er sonst ist.

## Die 7 Pflicht-Elemente

1. **Branding-Footer** — letzte Zeile jeder SKILL.md, exakt dieser Wortlaut:

   ```
   ---
   *Ein Skill von KI-Wissen.org — Entwickler: Harald Frey · [ki-wissen.org](https://ki-wissen.org)*
   ```

   Eine Zeile, am Dateiende, keine längeren Herkunfts-Abschnitte (Token-Kosten bei jedem Aufruf).

2. **README-Pflicht** — jeder Skill hat eine `README.md` in Kundensprache
   (aus `readme-template.md`). Kein Skill verlässt das Haus ohne.

3. **CHANGELOG + Semver** — jeder Skill hat `CHANGELOG.md` und eine Versionsnummer
   nach `versionierung.md`.

4. **Geführte Entwicklung** — neue Skills entstehen im Interview-Modus
   (siehe Befehl 3): Claude fragt, Harald antwortet, ein Schritt nach dem anderen.

5. **Gegenprüfungs-Pflicht** — jede Idee/Vorgabe von Harald wird **sofort** gegen
   Audit-Checkliste (inkl. Block F: User-Sicht/UX) geprüft. Bedenken werden direkt
   geäußert — nicht erst beim Audit. Formulierung: kurz, konkret, mit Alternative.
   Harald entscheidet; seine Entscheidung wird umgesetzt und im CHANGELOG vermerkt.

6. **Exklusiv-Kennzeichnung** — jeder Skill hat eine Einstufung, sichtbar im REGISTER
   (Spalte „Vertrieb") und im README-Kopf:
   - `Community` — frei für alle KI-Wissen.org-Nutzer
   - `Pro` — exklusiv für zahlende Mitglieder
   - `Kunde: <Name>` — individuell für einen Kunden

7. **Einsteiger-Sprache + Support-Zeile** — Zielgruppe sind KI-Einsteiger, keine
   Entwickler. README ohne Jargon (Test: versteht jemand ohne Vorkenntnisse das
   Onboarding allein?). Jede README endet mit der einheitlichen Support-Zeile:

   ```
   ---
   Fragen oder Probleme? → https://ki-wissen.org · Ein Skill von KI-Wissen.org (Harald Frey)
   ```

## Portabilitäts-Report (Codex / Google Antigravity)

Skills folgen dem offenen Agent-Skills-Standard (agentskills.io), den Claude,
OpenAI Codex und Google Antigravity unterstützen. Volle automatische Tests laufen
nur in Cowork. Für die anderen Plattformen gilt:

**Bei jedem Test (Befehl 4) zusätzlich einen Portabilitäts-Report erstellen** —
statische Prüfung der SKILL.md auf Cowork-only-Annahmen:

| Prüfpunkt | Portabel? |
|---|---|
| Nur `name` + `description` im Frontmatter (Standard-Felder) | ✅ überall |
| `compatibility`-Feld | ⚠️ wird außerhalb Claude ignoriert |
| `AskUserQuestion`-Anweisungen | ❌ nur Cowork — Fallback nötig („frage im Chat") |
| `present_files`-Anweisungen | ❌ nur Cowork — Fallback: „nenne den Dateipfad" |
| Cowork-Ordner-Konzepte („Cowork-Ordner", „Speicher") | ❌ — neutral formulieren („Arbeitsordner") |
| Verweise auf andere installierte Skills (z.B. skill-creator) | ⚠️ plattformabhängig |
| Eingebettete Skripte (scripts/) | ✅ überall, wenn nur Standard-Python/Bash |

**Report-Format** (in den Testbericht aufnehmen):

```
## Portabilität
Cowork: ✅ voll getestet (n/n Fälle)
Codex / Antigravity: <✅ standardkonform | ⚠️ mit Einschränkungen: …>
Cowork-only-Features: <Liste oder „keine">
```

**Test-Prompt-Paket für manuelle Fremd-Tests:** Auf Wunsch („Test-Paket für Codex")
die Testfälle aus `evals.json` als Copy-Paste-Prompts in eine Datei
`evals/test-paket-extern-v<version>.md` schreiben — ein Prompt pro Testfall plus
Erwartung in einem Satz. Harald klickt sie in Codex/Antigravity durch und meldet
Ergebnisse über Befehl 7 (Feedback) zurück.

**Einordnung für Harald, falls er fragt:** Claude kann Codex und Antigravity nicht
selbst ausführen — das sind separate Apps. Der Portabilitäts-Report + das
Test-Paket sind der ehrliche, maximale Automatisierungsgrad.
