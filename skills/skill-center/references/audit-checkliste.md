# Audit-Checkliste

Beim Auswerten eines Skills jeden Punkt prüfen. Pro Skill eine Ampel (🟢/🟡/🔴) und priorisierte Vorschläge ableiten.

## A. Triggern (wichtigster Block)
- Hat der Skill eine `description` mit konkreten Trigger-Phrasen?
- Sind die Trigger „pushy" genug formuliert, damit der Skill nicht untertriggert?
- Ist die description in **dritter Person** geschrieben? (Sie landet im System-Prompt — Ich-/Du-Form stört die Erkennung.)
- Gibt es **Negativ-Abgrenzungen** („NICHT triggern bei …")? Pflicht, nicht nur bei offensichtlicher Verwechslungsgefahr — klare Grenzen verhindern Über-Triggern.
- Deckt die Beschreibung sowohl WAS der Skill tut als auch WANN er auslösen soll? Wichtigster Anwendungsfall und Trigger-Wörter am Anfang (falls die description gekürzt wird, bleibt das Wesentliche erhalten).

## B. Struktur & Frontmatter
- Gültiges YAML-Frontmatter mit `name` und `description`?
- `name` in kebab-case, ohne Leer-/Sonderzeichen?
- SKILL.md unter ~500 Zeilen? Falls länger: in `references/` ausgelagert mit klaren Verweisen?
- **Progressive Disclosure eingehalten?** Drei Ebenen: (1) name+description → (2) SKILL.md als „Inhaltsverzeichnis" → (3) references als „Kapitel". Inhalte, die nur in Spezialfällen gebraucht werden oder sich gegenseitig ausschließen, gehören in getrennte references-Dateien — nicht alle in die SKILL.md.
- **Ein Skill = ein Job?** Macht der Skill mehrere unabhängige Dinge (z.B. erstellen UND analysieren UND versenden)? → Aufteilung in fokussierte Einzel-Skills empfehlen.
- Bei komplexen Skills mit mehreren Pfaden: gibt es einen **Entscheidungsbaum** („Wenn Nutzer X erwähnt → Pfad A")?

## C. Inhalt & Klarheit
- Klare, imperativische Anweisungen statt Geschwafel?
- Definiertes Outputformat (Template/Struktur), wo ein festes Ergebnis erwartet wird?
- Mindestens 1–2 konkrete Beispiele (Eingabe → Ergebnis)?
- Werden benötigte Tools/Verbindungen (MCPs, Ordner) genannt?

## D. Kundentauglichkeit (für Verkauf entscheidend)
- Gibt es eine README.md für den Kunden?
- Versteht ein fremder Nutzer ohne Harald, wie er den Skill bedient?
- Keine internen Pfade, Namen oder Annahmen, die nur bei Harald gelten (außer gewollt)?
- Versionsnummer + CHANGELOG vorhanden?
- **KI-Wissen.org-Standard erfüllt?** Alle 7 Pflicht-Elemente aus `kiwissen-standard.md`: Branding-Footer (letzte Zeile der SKILL.md), README, CHANGELOG, Vertriebs-Einstufung, Support-Zeile, Einsteiger-Sprache.
- **Portabilität geprüft?** Cowork-only-Annahmen identifiziert und im Portabilitäts-Report vermerkt (siehe kiwissen-standard.md)?

## E. Testbarkeit
- Gibt es `evals/evals.json` mit Testfällen?
- Wann zuletzt getestet? Status freigegeben?
- **Mit welchem Modell getestet?** Ist seitdem ein neueres Modell aktiv → Retest empfehlen.
- Gibt es offene Einträge in `evals/feedback.md`? → In die Vorschläge einarbeiten.

## F. User-Sicht & UX-Design (Pflicht bei jedem Audit)
- Was sieht der Nutzer **zuerst**, wenn der Skill läuft? Funktioniert genau das zuverlässig?
- Funktionieren interaktive Elemente in der **echten Umgebung**? Die Cowork-Vorschau ist eine Sandbox: `window.open`, `localStorage` u.ä. sind blockiert — Buttons/Links nur mit nachweislich funktionierenden Mechanismen (z.B. einfache `<a href>`-Links).
- Sind **Klickwege kurz**? Wo möglich direkt zur Quelle verlinken (Mail, Aufgabe, Termin) statt den Nutzer suchen zu lassen.
- Stehen **Diagnose-/Technik-Texte** fälschlich im Endprodukt? Die gehören in den Chat; im Produkt nur kurze, nutzerfreundliche Meldungen.
- Passt der Output zum **Kontext des Nutzers** (Tageszeit, schmale Seitenleiste vs. Browser, Vergangenes vs. Kommendes)?
- Erzeugt der Skill Dateien → das **letzte reale Ergebnis** ansehen, nicht nur die SKILL.md bewerten.

## Ampel-Logik
- 🟢 kundenreif: A vollständig, B/C/D/F ok, getestet & freigegeben.
- 🟡 überarbeiten: funktioniert, aber es fehlen Doku, Beispiele, Tests, Trigger sind schwach oder UX-Mängel (Block F).
- 🔴 nicht kundenreif: ungültiges Frontmatter, keine/kaputte Trigger, kein klares Output, keine Doku, oder kaputte interaktive Elemente, die der Nutzer als Erstes sieht.

## Optimierungsvorschläge ableiten
Pro Skill konkret und priorisiert (Wirkung hoch/mittel/niedrig). Beispiele:
- „Trigger schärfen: Phrase X, Y ergänzen" (hoch)
- „Beispiel-Block für Standardfall ergänzen" (mittel)
- „README fehlt — vor Verkauf zwingend" (hoch)
- „SKILL.md 700 Zeilen → Abschnitt Z in references auslagern" (mittel)
