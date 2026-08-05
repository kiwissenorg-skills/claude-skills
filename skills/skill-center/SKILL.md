---
name: skill-center
description: >
  Haralds Kommandozentrale für Entwicklung, Auswertung, Versionierung, Testung,
  Dokumentation und Auslieferung von Skills für Kunden. IMMER nutzen, wenn Harald
  an seinen Skills arbeiten will — auswerten, verbessern, neu entwickeln, automatisch
  testen, dokumentieren, versionieren, ausliefern oder Feedback zu einem Skill erfassen.
  Trigger: "Skill-Center", "Skill auswerten", "Skills prüfen", "Skill-Audit", "Skill
  überarbeiten", "neuen Skill bauen", "Skill testen", "Testbericht", "Skill dokumentieren",
  "Skill ausliefern", "Skill verkaufen", "neue Version", "Skill freigeben", "welche Skills
  habe ich", "Skill-Register", "Skill hat falsch ausgelöst", "KI-Wissen-Standard",
  "Portabilität", "Video-Skript für den Skill", "Skill vorstellen". Auch triggern bei
  "mach meinen Skill fertig", "ist der Skill kundenreif",
  "optimiere Skill X", "lass uns gemeinsam einen Skill entwickeln", wenn Harald einen
  Fehlgriff eines Skills meldet oder einen Skill als Produkt professionalisieren will.
compatibility: Cowork-Desktop-App mit Zugriff auf den Speicher-Ordner. Nutzt den vorhandenen skill-creator als Test-Engine.
---

# Skill-Center

Die zentrale Werkbank für Haralds Skill-Geschäft. Hier werden Skills **ausgewertet, überarbeitet, neu entwickelt, getestet, dokumentiert, versioniert und kundenreif ausgeliefert**. Ziel: Harald soll Skills professionell an Kunden verkaufen können, ohne jedes Mal selbst stundenlang zu testen.

Der Leitgedanke: **Ein Skill verlässt das Skill-Center erst, wenn er getestet, dokumentiert und freigegeben ist.** Bis dahin trägt er den Status „in Arbeit".

---

## Sprache & Tonfall

Harald ist KI-Trainer, kein Programmierer im engeren Sinn. Sprich in klarer, verständlicher Sprache. Vermeide unnötigen Fachjargon. Wenn ein technischer Begriff nötig ist (z.B. „YAML-Frontmatter"), erkläre ihn in einem Halbsatz. Halte dich an Haralds Präferenz: prägnant, direkt, ohne Floskeln. Hake bei Unklarheiten nach.

---

## Arbeitsordner

Das Skill-Center arbeitet in einem festen Ordner im Speicher:

```
Speicher/Skill-Center/
├── REGISTER.md            # Zentrale Übersicht aller Skills (Status, Version, Datum, Kunde)
├── Skills/                # Aktuelle Arbeitsstände aller Skills (je ein Unterordner)
│   └── <skill-name>/
│       ├── SKILL.md
│       ├── README.md      # Kunden-Dokumentation
│       ├── CHANGELOG.md   # Versionshistorie
│       ├── evals/         # Testfälle (evals.json) + Testberichte + feedback.md
│       └── references/    # optionale Zusatzdateien des Skills
├── Archiv/                # Alte Versionen (eingefroren, nie überschrieben)
│   └── <skill-name>/v1.0/ ...
└── Auslieferung/          # Fertige, freigegebene Pakete (.skill / .plugin) für Kunden
    └── <skill-name>-v1.2.skill
```

**Beim ersten Start:** Prüfe, ob `Speicher/Skill-Center/` existiert. Wenn nicht, lege die Struktur an und erstelle ein leeres `REGISTER.md` aus der Vorlage in `references/register-template.md`.

---

## Die acht Befehle

Das Skill-Center kennt acht Kernbefehle. Harald muss sie nicht wörtlich sagen — erkenne die Absicht. Wenn unklar ist, was er will, frage kurz nach, welcher der Befehle gemeint ist.

| Befehl | Was passiert | Wann |
|---|---|---|
| **1. Auswerten** | Audit eines/aller Skills + Optimierungsvorschläge | „werte aus", „prüf meine Skills", „Audit" |
| **2. Überarbeiten** | Skill verbessern, neue Version, alte ins Archiv | „überarbeite", „optimiere Skill X", „v2" |
| **3. Neu bauen** | Neuen Skill aus Haralds Beschreibung erstellen (v1.0) | „bau einen Skill der …" |
| **4. Testen** | Eval-Suite ausführen, Testbericht, Freigabe-Status setzen | „teste", „Testbericht", „ist der fertig" |
| **5. Dokumentieren** | README für Kunden erzeugen/aktualisieren | „dokumentiere", „Kunden-Doku" |
| **6. Ausliefern** | Freigegebenen Skill als Paket für Kunden verpacken | „liefere aus", „Skill an Kunden", „verkaufsfertig" |
| **7. Feedback erfassen** | Fehlgriff/Beobachtung aus echter Nutzung loggen | „der Skill hat falsch ausgelöst", „Feedback", „merk dir das" |
| **8. Video-Skript** | Vorstellungs-Skript aus SKILL.md + README erzeugen (nur freigegebene Skills) | „Video-Skript", „Skript fürs Video", „Skill vorstellen" |

Daneben gibt es jederzeit den **Register-Befehl** („zeig mir meine Skills", „Übersicht") → siehe Abschnitt Register.

---

## Befehl 1 — Auswerten (Audit)

Ziel: Harald bekommt eine ehrliche Qualitäts-Einschätzung seiner Skills **plus konkrete Optimierungsvorschläge**, die du selbst erkennst — nicht nur wenn er danach fragt.

**Ablauf:**

1. Frage, ob ein einzelner Skill oder alle ausgewertet werden sollen.
2. Lies für jeden Skill die `SKILL.md`. Bewerte anhand der Audit-Checkliste in `references/audit-checkliste.md`.
3. Vergib pro Skill eine **Ampel**:
   - 🟢 kundenreif (kleine oder keine Mängel)
   - 🟡 brauchbar, aber überarbeiten vor Verkauf
   - 🔴 nicht kundenreif (gravierende Lücken)
4. Liste pro Skill **konkrete, priorisierte Optimierungsvorschläge** (Wirkung: hoch / mittel / niedrig). Sei proaktiv: schlage Verbesserungen vor, auch wenn Harald nicht explizit danach fragt — Trigger-Schärfung, fehlende Beispiele, fehlende Doku, fehlende Tests, zu lange/zu kurze SKILL.md, unklare Outputformate, fehlende Progressive Disclosure, mehrere Jobs in einem Skill.
4b. **Feedback einbeziehen:** Existiert `evals/feedback.md` beim Skill, die offenen Einträge lesen und in die Vorschläge einarbeiten — Feedback aus echter Nutzung ist das stärkste Verbesserungssignal.
4c. **UX-Review:** Jeden Skill zusätzlich aus User-Sicht prüfen (Block F der Audit-Checkliste): Was sieht der Nutzer zuerst? Funktionieren interaktive Elemente in der Cowork-Sandbox? Sind Klickwege kurz? Stehen Diagnose-Texte fälschlich im Endprodukt?
5. Gib das Ergebnis als Markdown-Tabelle aus (Skill | Ampel | Top-Mangel | Empfehlung) plus darunter die Detailliste je Skill.
6. Aktualisiere im REGISTER den Status und das Audit-Datum.

**Wichtig:** Beim Auswerten wird **nichts verändert**. Du gibst nur die Bewertung + Vorschläge aus. Das Umsetzen passiert erst über Befehl 2 (Überarbeiten), wenn Harald grünes Licht gibt.

---

## Befehl 2 — Überarbeiten (neue Version)

Ziel: Einen bestehenden Skill verbessern und dabei sauber versionieren — alte Version geht nie verloren.

**Ablauf:**

1. Lege die aktuelle Version **vor jeder Änderung** im Archiv ab: `Archiv/<skill-name>/v<alt>/`. Niemals die alte Version überschreiben.
2. Bestimme die neue Versionsnummer nach den Regeln in `references/versionierung.md` (Semver: MAJOR.MINOR.PATCH).
3. Nimm die Verbesserungen vor. Bei größeren Umbauten arbeite abschnittsweise und zeige Harald Zwischenstände.
4. Trage die Änderung in `CHANGELOG.md` des Skills ein (Version, Datum, was geändert wurde).
5. Setze den Skill-Status auf **„in Arbeit"** — er muss nach jeder Überarbeitung neu getestet werden (Befehl 4), bevor er wieder freigegeben werden kann.
6. Aktualisiere das REGISTER.

Für die eigentliche inhaltliche Verbesserung von SKILL.md-Texten, Trigger-Beschreibungen und Struktur nutze die Logik des `skill-creator` (Skill-Writing-Guide, Description-Improver). Das Skill-Center ersetzt den skill-creator nicht — es steuert ihn und ergänzt Versionierung, Testung, Doku und Auslieferung darum herum.

**Description-Optimierung als eigener Schritt:** Wenn die Überarbeitung die `description` betrifft (Trigger-Probleme, Unter-/Übertriggern), den **Description-Improver des skill-creator** aktiv einsetzen: Test-Prompts aus der `evals.json` als Eingabe verwenden, mehrere Description-Varianten gegeneinander prüfen lassen und die beste übernehmen. Dabei die Pflichtkriterien aus der Audit-Checkliste (Block A) einhalten: dritte Person, WAS + WANN, „pushy" Trigger, klare „NICHT triggern bei …"-Abgrenzung.

**Progressive Disclosure beim Umbau:** Wird die SKILL.md zu groß oder enthält sie Inhalte, die nur in bestimmten Fällen gebraucht werden (z.B. Spezial-Workflows, lange Vorlagen), diese in `references/` auslagern und in der SKILL.md nur kurz verweisen. Leitbild: Die SKILL.md ist das Inhaltsverzeichnis, die references sind die Kapitel. Inhalte, die sich gegenseitig ausschließen, gehören in getrennte Dateien.

---

## Befehl 3 — Neu bauen (geführte Entwicklung)

Ziel: Aus Haralds Beschreibung einen neuen, kundentauglichen Skill als **v1.0** erstellen — **gemeinsam, im Interview-Modus**. Claude führt durch den Prozess, Harald antwortet; jeder Schritt einzeln über `AskUserQuestion`, keine Fragen-Blöcke. Der Skill muss am Ende den **KI-Wissen.org-Standard** erfüllen (`references/kiwissen-standard.md`).

**Interview-Schritte (in dieser Reihenfolge, je ein Schritt pro Frage):**

1. **Job:** Was soll der Skill können? (Eine Aufgabe — bei mehreren: Aufteilung vorschlagen, Ein-Skill-ein-Job.)
2. **Auslöser:** Bei welchen Sätzen/Situationen soll er triggern? Wobei ausdrücklich NICHT?
3. **Eingaben & Ergebnis:** Was gibt der Nutzer hinein, was kommt heraus (Format)?
4. **Zielgruppe & Vertrieb:** Community / Pro (exklusiv) / einzelner Kunde? Versteht ein KI-Einsteiger das Onboarding allein?
5. **Beispiele:** 1–2 echte Beispiel-Eingaben von Harald.
6. **Zusammenfassung zur Freigabe:** Alle Antworten kompakt zeigen, Harald bestätigt oder korrigiert — erst dann bauen.

**Gegenprüfungs-Pflicht (gilt in jedem Schritt):** Jede Idee oder Vorgabe von Harald sofort gegen die Audit-Checkliste prüfen — besonders Block F (User-Sicht/UX) und die Sandbox-Grenzen. Bedenken direkt äußern: kurz, konkret, mit Alternative. Beispiel: „Dein Button-Wunsch funktioniert in der Cowork-Vorschau nicht (Sandbox blockiert window.open) — Alternative: file://-Link." Harald entscheidet.
**Nach der Freigabe — Skill erstellen:**

2. Erstelle den Skill-Ordner unter `Skills/<skill-name>/` mit:
   - `SKILL.md` (sauberes Frontmatter, „pushy" formulierte Trigger gegen Untertriggern, description in dritter Person mit WAS + WANN + „NICHT triggern bei …", **Branding-Footer als letzte Zeile** — Wortlaut in `references/kiwissen-standard.md`)
   - `evals/evals.json` mit 2–3 realistischen Testfällen (aus dem Template `references/eval-template.json`)
   - `README.md` (Kunden-Doku in Einsteiger-Sprache, aus `references/readme-template.md`, mit Vertriebs-Einstufung im Kopf und Support-Zeile am Ende)
   - `CHANGELOG.md` mit Eintrag „v1.0 — Erstellt am <Datum>"
3. Setze Version **v1.0**, Status **„in Arbeit"**, Vertriebs-Einstufung ins REGISTER.
4. Schlage Harald sofort vor, jetzt zu testen (Befehl 4).
5. Trage den neuen Skill ins REGISTER ein.

Halte die `SKILL.md` unter ~500 Zeilen. Lagere große Zusatzinhalte in `references/` aus und verweise von der SKILL.md darauf (Progressive Disclosure: SKILL.md = Inhaltsverzeichnis, references = Kapitel).

**Entscheidungsbäume bei komplexen Skills:** Hat der Skill mehrere Pfade (z.B. unterschiedliche Outputs je nach Eingabe), einen kurzen Entscheidungsbaum in die SKILL.md schreiben: „Wenn der Nutzer X erwähnt → Pfad A. Wenn Y → Pfad B." Das macht das Verhalten vorhersagbar und testbar.

---

## Befehl 4 — Testen (der Kern)

Ziel: Den Skill **automatisch und objektiv** prüfen, einen **Testbericht** erzeugen und den Freigabe-Status setzen. Harald soll nicht mehr selbst testen müssen.

**Testmethode: Eval-Suite mit Testfällen.** Jeder Skill hat eine `evals/evals.json` mit Testfällen. Ein Testfall besteht aus einer realistischen Eingabe und prüfbaren Erwartungen (triggert der Skill? enthält der Output die geforderten Teile? stimmt das Format?).

**Ablauf:**

1. Wenn noch keine `evals.json` existiert oder zu dünn ist: erstelle 3–5 Testfälle aus dem Template `references/eval-template.json`. Decke ab: (a) klare Trigger-Fälle, (b) ein Grenzfall, (c) optional ein Fall, der NICHT triggern soll (Über-Triggern vermeiden).
2. Führe die Tests über einen **Test-Subagenten** aus (Agent-Tool, `general-purpose`), damit der Haupt-Kontext sauber bleibt. **Subagenten mit Modell `sonnet` starten** (Model-Parameter des Agent-Tools) — Sonnet ist die Referenz, weil die meisten KI-Wissen-User damit arbeiten; ein Skill muss mit Sonnet funktionieren, nicht nur mit Opus. Der Subagent bekommt: den Skill-Inhalt, die Testfälle und die Bewertungsregeln aus `references/test-protokoll.md`. Bei mehreren unabhängigen Skills mehrere Subagenten parallel starten.
3. Der Subagent bewertet jeden Testfall **bestanden / durchgefallen** mit Begründung und liefert die Ergebnisse zurück. **Trigger-Tests mehrfach laufen lassen:** Ob ein Skill auslöst ist nicht deterministisch — jeden Trigger-Fall **3× simulieren** und eine **Trigger-Quote** erfassen (z.B. 3/3, 2/3). Erst ab 3/3 gilt der Trigger-Teil als bestanden; 2/3 = wackelig → Description schärfen (Description-Improver, siehe Befehl 2).
4. Erzeuge daraus den **Testbericht** nach der Vorlage in `references/test-protokoll.md` und speichere ihn als `evals/testbericht-v<version>-<datum>.md`.
4b. **Portabilitäts-Report** in den Testbericht aufnehmen: statische Prüfung auf Cowork-only-Annahmen nach `references/kiwissen-standard.md` (Abschnitt Portabilitäts-Report). Volle automatische Tests laufen nur in Cowork; für Codex/Google Antigravity wird Standardkonformität geprüft. Auf Wunsch zusätzlich das **Test-Prompt-Paket** für manuelle Fremd-Tests erzeugen (`evals/test-paket-extern-v<version>.md`).
5. **Freigabe-Logik:**
   - Alle Tests bestanden → Status **„freigegeben ✅"**. Skill darf ausgeliefert werden.
   - Mindestens ein Test durchgefallen → Status bleibt **„in Arbeit"**. Gib die Liste der Fehler aus und schlage konkrete Fixes vor. Biete an, direkt zu überarbeiten (Befehl 2) und danach erneut zu testen.
6. Aktualisiere REGISTER (Status, Testdatum, Trefferquote, **getestet mit Modell** — z.B. „Opus 4.6").

**Retest bei Modell-Updates:** Skills verhalten sich nach einem Modellwechsel anders. Deshalb: Im REGISTER steht pro Skill, mit welchem Modell zuletzt getestet wurde. Fällt beim Arbeiten auf, dass das aktuelle Modell neuer ist als das im REGISTER vermerkte, Harald proaktiv darauf hinweisen: „Skill X wurde zuletzt mit Modell Y getestet — empfehle Retest." Grundregel: **Neues Modell = alle freigegebenen Skills neu testen.**

**Ehrliche Grenze, die du Harald nennen sollst, falls relevant:** Eval-Tests prüfen Triggern und Output-Struktur sehr zuverlässig. Sie können **subjektive Qualität** (Tonfall, „gefällt es dem Kunden") nicht garantieren. Markiere im Testbericht klar, was automatisch geprüft wurde und was ein letzter menschlicher Blick abdecken sollte. Verkaufe „freigegeben" nie als absolute Garantie für Geschmacksfragen.

---

## Befehl 5 — Dokumentieren (Kunden-README)

Ziel: Jeder ausgelieferte Skill bekommt eine **README.md**, mit der der Kunde allein klarkommt — ohne Harald zu fragen.

Erzeuge/aktualisiere `Skills/<skill-name>/README.md` aus `references/readme-template.md`. Inhalt:

- Was der Skill tut (in Kundensprache, kein Jargon)
- Welche Trigger / Beispielsätze ihn auslösen
- Schritt-für-Schritt-Installation
- 2–3 Anwendungsbeispiele (Eingabe → Ergebnis)
- Voraussetzungen / benötigte Verbindungen
- Versionsstand + kurze Was-ist-neu-Notiz
- Mini-Troubleshooting („Skill reagiert nicht? → …")
- Kontakt/Support-Zeile (Haralds Daten)

Die README wird automatisch bei „Neu bauen" und vor jeder „Auslieferung" mitgepflegt — Harald muss sie nicht extra anfordern.

---

## Befehl 6 — Ausliefern

Ziel: Einen **freigegebenen** Skill als installierbares Paket für den Kunden verpacken.

**Vorbedingung — strikt:** Nur Skills mit Status **„freigegeben ✅"** dürfen ausgeliefert werden. Hat der Skill diesen Status nicht, weigere dich und biete an, erst zu testen (Befehl 4).

**Ablauf:**

1. Prüfe Status im REGISTER. Wenn nicht freigegeben → stoppen, Harald informieren.
2. Stelle sicher, dass README.md aktuell ist (sonst Befehl 5).
2a. **KI-Wissen.org-Standard-Check (Pflicht):** Alle 7 Pflicht-Elemente aus `references/kiwissen-standard.md` prüfen — Branding-Footer, README, CHANGELOG, Vertriebs-Einstufung, Support-Zeile, Einsteiger-Sprache. Fehlt etwas → erst nachrüsten, dann ausliefern.
2b. **Security-Check (Pflicht vor jeder Auslieferung):** Kunden installieren Haralds Pakete in ihrer Umgebung — der Inhalt muss sauber sein. Kurz prüfen:
   - Keine Anweisungen im Skill, die Daten an externe Adressen senden oder unbekannte Quellen laden.
   - Mitgelieferte Skripte gesichtet: tun sie nur, was die Doku sagt? Keine versteckten Netzwerkzugriffe.
   - Keine internen Daten von Harald im Paket (Pfade, Kundennamen, API-Schlüssel, E-Mail-Adressen außer der Support-Zeile). **Insbesondere: niemals `cloudflare-r2.md` oder andere Zugangsdaten-Dateien im Paket.**
   - Ergebnis als eine Zeile im Testbericht/REGISTER vermerken: „Security-Check bestanden <Datum>".
3. Verpacke den Skill. Zwei Formate je nach Kundenwunsch:
   - **`.skill`** (einzelner Skill als ZIP des Skill-Ordners mit SKILL.md + README + references) — für Kunden, die einen einzelnen Skill installieren.
   - **`.plugin`** (mehrere Skills gebündelt mit `.claude-plugin/plugin.json`) — wenn Harald mehrere Skills als Paket/Marketplace an einen Kunden gibt.
   Frage im Zweifel, welches Format. Details in `references/auslieferung.md`.
4. Lege das Paket in `Auslieferung/<skill-name>-v<version>.skill` (bzw. `.plugin`).
5. Präsentiere Harald die fertige Datei mit `present_files`, damit er sie direkt weitergeben kann.
6. **Veröffentlichung auf Cloudflare R2** (für exklusive Skills, die per Download-Link an User gehen): Upload mit dem Skript `Speicher/Skill-Center/r2-upload.py` nach `references/veroeffentlichung-r2.md` — stabiler Link + versioniertes Archiv, korrekte Header, Link-Verifikation. Den fertigen User-Link nennen.
7. Vermerke im REGISTER: ausgeliefert am <Datum>, an Kunde <X>, Version <v>, ggf. Download-Link.

---

## Befehl 7 — Feedback erfassen

Ziel: Beobachtungen aus echter Nutzung festhalten — das stärkste Signal für Verbesserungen. Typische Fälle: ein Skill hat nicht ausgelöst obwohl er sollte, hat fälschlich ausgelöst, oder das Ergebnis war daneben.

**Ablauf:**

1. Harald meldet einen Fehlgriff (z.B. „der Angebots-Skill hat bei einer Rechnung ausgelöst") oder eine Beobachtung.
2. Eintrag in `Skills/<skill-name>/evals/feedback.md` anhängen (Format und Regeln: `references/feedback-template.md`): Datum, was passiert ist, erwartetes vs. tatsächliches Verhalten, Einordnung (description / Verhalten / UX), Status „offen".
3. Sofort kurz einordnen: Liegt es an der description (Triggern) oder am Skill-Inhalt (Verhalten)? Einen konkreten Fix vorschlagen — aber **nichts ohne Haralds OK ändern**.
4. Wenn der Fix übernommen werden soll → Befehl 2 (Überarbeiten); aus dem Fehlgriff zusätzlich einen neuen Testfall in `evals.json` machen, damit derselbe Fehler nie wieder unbemerkt passiert. Eintrag in feedback.md auf „behoben in v<x>" setzen.
5. Beim nächsten Audit (Befehl 1) werden offene Feedback-Einträge automatisch berücksichtigt.

---

## Befehl 8 — Video-Skript

Ziel: Für einen **freigegebenen** Skill das Skript für Haralds Vorstellungsvideo erzeugen — automatisch aus SKILL.md, README und CHANGELOG, im Stil seines Mustertexts.

**Vorbedingung:** Status „freigegeben ✅". Sonst Hinweis und Abbruch — Videos beschreiben nur stabile Funktionen.

**Ablauf:** Struktur, Stilmerkmale und Schritte stehen in `references/video-skript-template.md` (5 Teile: Nutzenversprechen → Besonderheit → Installation → Demo-Durchlauf → Zusammenfassung; Du-Ansprache, Fließtext, 350–550 Wörter). Skript speichern als `Skills/<skill-name>/video-skript-v<version>.md`, im REGISTER vermerken.

**Abgrenzung:** Befehl 8 liefert das **Rohskript**. Teleprompter-Optimierung und docx-Export übernehmen Haralds bestehende Skills `youtube-skript` / `ki-videotutorials` — darauf am Ende hinweisen, nicht duplizieren.

---

## Register-Befehl — Übersicht behalten

Bei „zeig mir meine Skills" / „Übersicht" / „Status": Lies `REGISTER.md` und gib eine kompakte Tabelle aus:

| Skill | Version | Status | Letzter Test | Modell | Vertrieb | Kunde | Ausgeliefert |

So behält Harald bei vielen Kundenskills den Überblick — wichtig, sobald er das professionell verkauft. Das REGISTER ist die einzige Wahrheit über den Stand aller Skills; halte es nach **jedem** Befehl aktuell.

---

## Goldene Regeln (immer beachten)

1. **Nie eine alte Version überschreiben** — immer erst ins Archiv.
2. **Nur freigegebene Skills ausliefern** — kein Verkauf von Ungetestetem.
3. **Doku gehört dazu** — kein Skill verlässt das Haus ohne README.
4. **Proaktiv optimieren** — Schwächen ansprechen, auch ungefragt, aber nichts ohne Haralds OK verändern.
5. **REGISTER immer aktuell halten.**
6. **Bei Unklarheit nachfragen** — lieber eine kurze Frage als die falsche Annahme.
7. **Ein Skill = ein Job** — bei mehreren Aufgaben Aufteilung vorschlagen.
8. **Jeden Skill aus User-Sicht und UX-Design-Perspektive betrachten** — bei Erstellung UND jeder Änderung: Was sieht der Nutzer zuerst? Was klickt er? Funktioniert das in der echten Umgebung (Cowork-Sandbox blockiert z.B. `window.open` und `localStorage`)? Diagnose-Texte gehören in den Chat, nicht ins Endprodukt.
9. **Neues Modell = Retest** — freigegebene Skills nach Modell-Updates neu testen.
10. **Fehlgriffe werden Testfälle** — jedes gemeldete Fehlverhalten landet in feedback.md und als neuer Eval-Fall.
11. **KI-Wissen.org-Standard ist Pflicht** — die 7 Elemente aus `references/kiwissen-standard.md` gelten für jeden Skill; ohne sie keine Auslieferung.
12. **Haralds Ideen werden sofort gegengeprüft** — Bedenken direkt äußern, kurz und mit Alternative; Harald entscheidet.

---

## Änderungshistorie

**1.3.1** — R2-Veröffentlichung (Juni 2026).
- Neu: Automatischer Upload exklusiver Skills auf Cloudflare R2 als Schritt 6 der Auslieferung — Skript `r2-upload.py` mit ZIP-Check, korrekten Download-Headern (gegen Umbenennen/Anzeigen im Browser), stabilem Link (`skills/<name>.skill`, no-cache) + versioniertem Archiv. Details: `references/veroeffentlichung-r2.md`.
- Neu: Download-&-Installations-Hinweisblock für User-READMEs (inkl. Safari-Auto-Entpacken).
- Security-Check ergänzt: Zugangsdaten-Dateien dürfen nie ins Paket.

**1.3.0** — Video-Skript (Juni 2026).
- Neu: Befehl 8 „Video-Skript" — erzeugt für freigegebene Skills automatisch das Vorstellungs-Skript aus SKILL.md + README + CHANGELOG, nach Haralds 5-Teile-Muster (`references/video-skript-template.md`). Rohskript-Übergabe an youtube-skript/ki-videotutorials für Teleprompter und docx.

**1.2.1** — Modell-Vorgabe (Juni 2026).
- Neu: Test-Subagenten laufen immer mit `model: sonnet` — Sonnet ist Freigabe-Referenz (Modell der meisten KI-Wissen-User). Entwickeln weiterhin mit dem stärksten Modell. Details in `references/test-protokoll.md`.

**1.2.0** — KI-Wissen.org-Standard (Juni 2026).
- Neu: `references/kiwissen-standard.md` — 7 Pflicht-Elemente für jeden Skill (Branding-Footer, README, CHANGELOG, geführte Entwicklung, Gegenprüfung, Exklusiv-Kennzeichnung, Einsteiger-Sprache + Support-Zeile).
- Neu: Befehl 3 als geführtes Interview — 6 Schritte, ein Schritt pro Frage, Zusammenfassung zur Freigabe vor dem Bauen.
- Neu: Gegenprüfungs-Pflicht — jede Vorgabe von Harald wird sofort gegen Audit-Checkliste + UX-Block geprüft, Bedenken mit Alternative.
- Neu: Portabilitäts-Report bei jedem Test — statische Prüfung auf Cowork-only-Annahmen (Codex/Antigravity-Standardkonformität); optionales Test-Prompt-Paket für manuelle Fremd-Tests.
- Neu: Vertriebs-Einstufung (Community / Pro / Kunde) im REGISTER und README.
- Neu: Standard-Check als Pflichtschritt vor jeder Auslieferung.

**1.1.0** — Best-Practice-Update (Juni 2026), basierend auf den offiziellen Leitlinien von Anthropic (Agent Skills), OpenAI (Codex Skills) und Google (Antigravity):
- Neu: Befehl 7 „Feedback erfassen" — Fehlgriffe aus echter Nutzung werden geloggt (`evals/feedback.md`) und automatisch zu Regressions-Testfällen.
- Neu: Trigger-Tests laufen 3× pro Fall (Trigger-Quote statt Einmal-Urteil) — Triggern ist nicht deterministisch.
- Neu: Modell-Tracking im REGISTER + Retest-Empfehlung bei Modell-Updates.
- Neu: Security-Check als Pflichtschritt vor jeder Auslieferung.
- Neu: UX-Review (Block F der Audit-Checkliste) — jeder Skill wird aus User-Sicht geprüft.
- Neu: Description-Improver des skill-creator als expliziter Schritt bei Trigger-Problemen.
- Audit-Checkliste erweitert: Progressive Disclosure, Ein-Skill-ein-Job, dritte Person, Pflicht-Negativ-Abgrenzungen, Trigger-Wörter am Anfang, Entscheidungsbäume.
- Neue Referenzdatei: `references/feedback-template.md`.

**1.0.0** — Erste Version (Juni 2026). Sechs Kernbefehle, Register, Versionierung, Eval-Tests, Kunden-README, Auslieferung.

---
*Ein Skill von KI-Wissen.org — Entwickler: Harald Frey · [ki-wissen.org](https://ki-wissen.org)*
