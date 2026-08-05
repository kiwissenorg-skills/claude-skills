---
name: morgen-dashboard
version: 1.0.0
description: Erstellt ein kompaktes Tages-Dashboard als HTML-Datei mit Kalender, Aufgaben, Inbox, Wetter und News. Ein Skill von KI-Wissen.org. Aktivieren bei: "Morgen-Dashboard", "Tages-Dashboard", "Dashboard für heute", "zeig mir mein Dashboard", "Tagesstart", "Morgenroutine", "plane meinen Tag", "was liegt heute an", "Daily Briefing", "Überblick für heute".
---

# Morgen-Dashboard

Ein Skill von **KI-Wissen.org** für die Community.

Erstellt ein ruhiges, übersichtliches Tages-Dashboard für den persönlichen Start in den Tag. Das Ergebnis ist eine einzelne HTML-Datei, die Claude dem Nutzer direkt zum Öffnen bereitstellt.

Das Ziel ist nicht, möglichst viele Informationen anzuzeigen, sondern die wichtigsten Entscheidungen für den Tag sichtbar zu machen.

---

## Ablauf (Schritt für Schritt)

1. **Einstellungen laden.** Prüfen, ob im Cowork-Ordner ein Ordner `Meine Dashboard-Einstellungen` mit einer gefüllten `einstellungen.md` existiert. Wenn ja, daraus Ort, News-Themen und bevorzugte Abschnitte übernehmen.
2. **Erster Start erkennen.** Fehlt der Ordner oder die Datei, Onboarding durchführen (siehe unten).
3. **Heutiges Dashboard prüfen.** Gibt es im Cowork-Ordner bereits eine Datei die mit `morgen-dashboard-YYYY-MM-DD` beginnt (also heutiges Datum), sofort mit `AskUserQuestion` fragen:

   > „Es gibt bereits ein Dashboard von heute ([Uhrzeit des Erstellungszeitpunkts]). Möchtest du das bestehende öffnen — das geht sofort — oder ein neues erstellen mit aktuellen E-Mails und Terminen?"

   Optionen: **Bestehendes öffnen** (schnell, Daten vom Erstellungszeitpunkt) / **Neu erstellen** (aktuell, dauert etwas länger)

   - Bei „Bestehendes öffnen": Die vorhandene HTML-Datei direkt mit `present_files` zeigen. Fertig — Schritte 4–6 überspringen.
   - Bei „Neu erstellen": Weiter mit Schritt 4. Die neue Datei bekommt einen neuen Zeitstempel im Namen.

4. **Datenquellen prüfen.** Welche Integrationen (Kalender, Mail, Aufgaben) sind verfügbar? Fehlende Daten beim Nutzer knapp nachfragen oder als fehlend markieren.
5. **Tag priorisieren.** Tagesfokus aus allen verfügbaren Daten ableiten.
6. **HTML-Datei erzeugen.** Datei mit Datum **und Uhrzeit** im Namen speichern: `morgen-dashboard-YYYY-MM-DD-HHmm.html` (z.B. `morgen-dashboard-2026-06-03-0742.html`) in den verbundenen Cowork-Ordner. So sind mehrere Versionen eines Tages unterscheidbar. Beim Speichern auch den Zeitstempel als sichtbares Element in die HTML-Kopfzeile einbauen (z.B. „Erstellt: 07:42 Uhr").
7. **Alte Dateien aufräumen.** Nach dem Speichern der neuen Datei: alle Dashboard-Dateien im Cowork-Ordner die älter als 7 Tage sind (`morgen-dashboard-*`) löschen. Dabei nur Dateien mit diesem exakten Namensmuster anfassen.
8. **Datei zeigen.** Die fertige HTML-Datei dem Nutzer mit `present_files` bereitstellen.
9. **Im Browser öffnen (automatisch).** Direkt danach das Dashboard im Browser des Nutzers öffnen — die Vorschau in der Desktop-App ist nur eine schmale Seitenleiste, volle Breite gibt es nur im Browser:
   - **Bevorzugter Weg:** Die Claude-in-Chrome-Browsertools nutzen (Tool `navigate`, bei Bedarf vorher per ToolSearch laden). Als URL den absoluten Dateipfad als `file://`-URL übergeben, Leerzeichen als `%20` kodieren. Beispiel: `file:///Users/name/Cowork-Ordner/morgen-dashboard-2026-06-05-0742.html`. Vorher mit `tabs_create_mcp` einen neuen Tab anlegen, damit kein bestehender Tab des Nutzers überschrieben wird.
   - **Fallback (Chrome-Erweiterung nicht verbunden):** Nicht still scheitern. Kurzer Chat-Hinweis mit dem eingebauten Klickweg der Vorschau:

     > „Für die volle Breite: Öffne das Dashboard über die Datei-Karte, klicke dann oben rechts in der Vorschau auf das Pfeil-Menü (∨) neben „Im Ordner anzeigen" und wähle **„In Google Chrome öffnen"**."

   Wichtig: Kein „Im Browser öffnen"-Button in der HTML-Datei. Die Cowork-Vorschau läuft in einer Sandbox, die sowohl JavaScript-Navigation (`window.open`) als auch `file://`-Links blockiert — ein solcher Button wäre ein toter Button.

---

## Onboarding beim ersten Start

Wenn kein Ordner `Meine Dashboard-Einstellungen` existiert, **vor** dem ersten Dashboard kurz onboarden:

1. Den leeren Ordner `Meine Dashboard-Einstellungen` im Cowork-Ordner anlegen.
2. Eine leere `einstellungen.md` mit Vorlage hineinlegen (siehe unten).
3. Den Nutzer freundlich begrüßen und in 2–3 Sätzen erklären, was der Skill braucht:

> „Ich bin dein Morgen-Dashboard. Beim ersten Start brauche ich kurz ein paar Infos von dir — dauert 30 Sekunden. Danach merke ich mir alles für die nächsten Male."

4. Mit `AskUserQuestion` aktiv abfragen — in dieser Reihenfolge:

   **Frage 1 — Ort:** Für Wetter, z.B. „München".

   **Frage 2 — Integrationen aktiv nutzen:** Welche der erkannten Integrationen sollen für das Dashboard verwendet werden? Erkannte Integrationen vorher prüfen (z.B. Gmail, Notion, Google Calendar) und als Optionen zur Auswahl anbieten. Nicht einfach annehmen, dass alle aktiven Integrationen gewünscht sind — explizit bestätigen lassen.

   **Frage 3 — Inbox-Einstellungen (nur wenn Gmail oder eine andere Mail-Integration ausgewählt):**
   - Wie viele Mails sollen maximal angezeigt werden? (Standard: 5)
   - Sollen nur Mails eines bestimmten Labels/Ordners berücksichtigt werden? (z.B. „Posteingang", „Wichtig", „[Gmail]/Starred" — oder „alle")

   **Frage 4 — Aufgaben-Einstellungen (nur wenn Notion oder ein anderes Aufgaben-Tool ausgewählt):**
   - Welche Notion-Datenbank soll für Aufgaben genutzt werden? Verfügbare Datenbanken zuerst über die Notion-Integration abfragen und als Auswahloptionen anzeigen. Nicht einfach die erste Datenbank nehmen — immer explizit bestätigen lassen.
   - Nur fällige Aufgaben oder auch bald fällige (nächste 3 Tage)?

   **Frage 5 — News-Themen:** Z.B. „KI, Automatisierung, Wirtschaft" — oder „keine".

   **Frage 6 — Abschnitte:** Welche Abschnitte sollen immer erscheinen? (Kalender / Aufgaben / Inbox / News / Wetter)

5. **Wichtiger Hinweis am Ende des Onboardings** (immer anzeigen, bevor das erste Dashboard erstellt wird):

> „Alles gespeichert! Du kannst jederzeit Integrationen ergänzen oder ändern — sag einfach z.B. „füge Notion hinzu" oder „ändere meine Einstellungen". Ich passe das Dashboard dann sofort an."

6. Antworten in `einstellungen.md` speichern und direkt das erste Dashboard erstellen.

**Inhalt der `einstellungen.md`-Vorlage** (beim Anlegen hineinschreiben):

```markdown
# Meine Dashboard-Einstellungen

## Ort (für Wetter)
<!-- z.B. München -->

## News-Themen
<!-- z.B. KI, Automatisierung, Wirtschaft — oder "keine" -->

## Bevorzugte Abschnitte
<!-- Kalender, Aufgaben, Inbox, News, Wetter — nicht gewünschte einfach löschen -->
- Kalender
- Aufgaben
- Inbox
- Wetter
- News

## Tool-Zuordnung
<!-- Welches Tool soll für welchen Bereich genutzt werden?
     Funktioniert mit jeder verbundenen Integration — Google, Microsoft, Notion, Apple usw.
     Wenn leer, nutzt der Skill automatisch alle verfügbaren Tools.
     Beispiele:
     Kalender: Outlook        (oder: Google Calendar, Apple Calendar, Notion …)
     Aufgaben: Microsoft Todo (oder: Notion, Asana, Trello, Linear …)
     Inbox: Outlook           (oder: Gmail, …)
-->
Kalender:
Aufgaben:
Inbox:

## Inbox-Einstellungen
<!-- Gilt für Gmail und andere Mail-Tools -->
Max. Mails anzeigen: 5
Label-Filter: <!-- z.B. "INBOX", "IMPORTANT", "Label_xyz" — leer = alle -->

## Aufgaben-Einstellungen
<!-- Gilt für Notion, Asana usw. -->
Notion-Datenbank: <!-- z.B. "Aufgaben" oder leer für automatische Auswahl -->
Zeitraum: <!-- "nur heute fällig" oder "nächste 3 Tage" -->

## Hinweise
<!-- Persönliche Präferenzen, z.B. "Inbox nur wenn mehr als 2 ungelesene" -->
```

**Einstellungen aktualisieren:** Sagt der Nutzer irgendwann „änder meinen Ort auf Berlin" oder „News brauch ich nicht mehr", die `einstellungen.md` entsprechend aktualisieren und kurz bestätigen.

---

## So nutzt du den Skill

Schreib einfach im Chat:

```text
Mach mir ein Morgen-Dashboard.
```

Oder mit eigenen Daten:

```text
Hier sind meine Termine, Mails und Aufgaben. Bau mir daraus ein Tages-Dashboard.
```

Wenn keine Kalender-, Mail- oder Aufgabenintegration verfügbar ist, kannst du die Daten direkt in den Chat einfügen:

```text
Ort: Hamburg
Termine:
- 09:00 Team-Call
- 13:30 Kundentermin mit ACME
Aufgaben:
- Angebot finalisieren
- Rechnung prüfen
Inbox:
- Mail von Anna: Rückfrage zum Vertrag, Antwort heute nötig
News-Themen: KI, Automatisierung, Datenschutz
```

---

## Wenn Nutzer nach der Funktionsweise fragen

Kurz erklären:

- Der Skill erstellt ein HTML-Dashboard für den heutigen Tag.
- Er merkt sich deine Einstellungen (Ort, News-Themen, Abschnitte) im Ordner `Meine Dashboard-Einstellungen`.
- Er nutzt verfügbare Daten aus Kalender, Inbox, Aufgaben, Wetter und optional News.
- Wenn kein Zugriff auf Datenquellen besteht, kann der Nutzer Daten manuell einfügen.
- Es werden keine Termine, Mails, Aufgaben oder News erfunden.
- Das Dashboard erscheint als klickbare Datei direkt im Chat.

In diesem Fall kein Dashboard erzeugen, außer der Nutzer fordert es danach ausdrücklich an.

---

## Kernprinzipien

- **Scanbar:** Der gesamte Inhalt muss in unter 60 Sekunden erfassbar sein.
- **Priorisiert:** Erst Fokus, dann Details.
- **Begrenzt:** Jeder Abschnitt hat ein klares Maximum.
- **Lokal:** HTML ist self-contained, ohne CDN, Tracking oder externe Assets.
- **Ehrlich:** Fehlende Daten werden als fehlend markiert oder der Abschnitt wird weggelassen.
- **Einfach:** Keine komplexen Automationspfade als Pflicht.

---

## Datenquellen

Nur Daten nutzen, die tatsächlich verfügbar sind. Der Skill funktioniert mit **jeder** verbundenen Integration — Google, Microsoft, Apple, Notion, Asana oder anderen. Es gibt keine Einschränkung auf bestimmte Anbieter.

**Tool-Priorität:** Ist in den Einstellungen eine Tool-Zuordnung hinterlegt (z.B. „Kalender: Outlook"), dieses Tool bevorzugt nutzen. Ist nichts hinterlegt, alle verfügbaren Integrationen für den jeweiligen Bereich verwenden.

1. **Kalender:** Termine des heutigen Tages — aus Outlook, Google Calendar, Apple Calendar, Notion oder einem anderen verbundenen Kalender.
2. **Aufgaben:** fällige, überfällige oder vom Nutzer markierte Aufgaben — aus Microsoft To-Do, Notion, Asana, Trello, Linear oder ähnlichem.
3. **Inbox:** E-Mails oder Nachrichten mit erkennbarem Handlungsbedarf — aus Outlook, Gmail oder einem anderen verbundenen Mail-Tool.
4. **Wetter:** kurzer Tagesausblick, wenn Ort (aus Einstellungen oder manuell) verfügbar ist.
5. **News:** optional, maximal 3 relevante Links mit Quelle — nur wenn Themen in Einstellungen hinterlegt.

Wenn keine Integrationen vorhanden sind, den Nutzer knapp um Eingabe bitten:

```text
Schick mir gern Termine, wichtige Mails und Aufgaben. Ich baue daraus ein kompaktes Tages-Dashboard.
```

---

## Abschnittslimits

- **Tagesfokus:** genau 3 Punkte, wenn genug Daten vorhanden; sonst 1–2.
- **Kalender:** maximal 7 Einträge, danach zusammenfassen.
- **Inbox:** maximal 5 Einträge mit Handlungsbedarf.
- **Aufgaben:** maximal 5 fällige oder wichtige Aufgaben.
- **Wetter:** 1 Zeile.
- **News:** maximal 3 Einträge.

Leere Abschnitte klein halten oder weglassen. Keine dekorativen Platzhalter.

---

## Dashboard-Struktur

**1. Kopfzeile**
- Begrüßung je nach Uhrzeit (vor 12 Uhr: „Guten Morgen.", 12–17 Uhr: „Guten Tag.", nach 17 Uhr: „Guten Abend.")
- Datum im deutschen Format: „Mittwoch, 3. Juni 2026"
- Wetter als kompakter Einzeiler, falls vorhanden.

**2. Tagesfokus**
- Die drei wichtigsten Prioritäten.
- Aus Kalender, Aufgaben, Inbox und Deadlines ableiten.
- Jede Priorität mit kurzem Grund.
- **Nur was noch ansteht:** Bereits vergangene Termine gehören nicht in den Tagesfokus. Wird das Dashboard nachmittags erstellt, den Fokus auf den Rest des Tages ausrichten.

**3. Nächster Schritt**
- Nächster Termin oder beste freie Fokuszeit.
- Falls der Tag leer ist: „Keine festen Termine gefunden."

**4. Kalender**
- Chronologische Liste.
- **Vergangene Termine ausgrauen** (z.B. `opacity: 0.5` plus Hinweis „vorbei") — sie stehen nicht gleichwertig neben kommenden Terminen.
- Kollisionen und Back-to-back-Termine markieren.
- Größere freie Blöcke hervorheben.

**5. Inbox und Aufgaben**
- Nur Dinge mit Handlungsbedarf.
- Kurze Aktion pro Eintrag: antworten, vorbereiten, entscheiden, warten, erledigen.
- Antwortvorschläge nur anbieten, wenn sie klar aus dem Kontext ableitbar sind.

**6. News (optional)**
- Nur relevante, aktuelle Meldungen.
- Immer mit Quelle.
- Weglassen, wenn keine Themen in Einstellungen hinterlegt oder keine Quellen verfügbar.

---

## Priorisierung

Sortieren nach:

1. Heute fällig oder zeitkritisch.
2. Blockiert andere Personen oder Projekte.
3. Braucht Vorbereitung vor einem Termin.
4. Ist wichtig, aber nicht dringend.

Optional eine kleine „Kann warten"-Zeile hinzufügen, wenn dadurch der Tag klarer wird.

---

## HTML-Anforderungen

Vollständige HTML-Datei mit inline CSS und inline JavaScript. Keine externen Abhängigkeiten.

**Gestaltung:**
- Einspaltiges Layout mit maximal 860px Breite.
- Basis-Schriftgröße mindestens 16px (body), Überschriften mindestens 18px, Karten-Inhalte mindestens 15px.
- Ausreichend Zeilenabstand (line-height: 1.6) und Padding in Karten (mindestens 16px).
- Ruhiger heller Hintergrund. **Standard ist immer der helle Modus** — kein automatisches `prefers-color-scheme`. Dark Mode nur über den manuellen Toggle (siehe Interaktion).
- Klare Karten oder Abschnitte mit dezenter Trennung.
- Gute Lesbarkeit auf Desktop und Mobile.
- Keine überladenen Farben.
- Keine langen Textblöcke.
- Statusfarben sparsam: Rot für dringend, Orange für Vorbereitung, Blau für Info, Grün für freie Zeit.

**Interaktion:**
- **Kein „Im Browser öffnen"-Button.** Die Cowork-Vorschau blockiert in ihrer Sandbox sowohl `window.open(...)` als auch `file://`-Links — jeder solche Button wäre dort funktionslos. Das Öffnen im Browser übernimmt Claude nach dem Erstellen automatisch (siehe Ablauf Schritt 9).
- **Hell/Dunkel-Toggle** oben rechts in der Kopfzeile: kleiner Umschalter (z.B. „🌙 / ☀️"), der per JavaScript die Klasse `dark` auf `<body>` setzt/entfernt. Standard ist hell. Kein `localStorage` (in der Sandbox blockiert) — der Toggle gilt nur für die aktuelle Ansicht. Implementierung: `<button class="toggle-btn" onclick="document.body.classList.toggle('dark')">🌙</button>`.
- **Abhak-Checkboxen** bei Tagesfokus und Aufgaben: jede Zeile bekommt eine native `<input type="checkbox">`. Abgehakte Einträge per CSS durchstreichen und ausgrauen (`li:has(input:checked) { text-decoration: line-through; opacity: 0.5; }`). Keine Speicherung — rein für die Session.
- **Klickbare Inbox-Einträge:** Wenn die Mail-Quelle Gmail ist, jeden Inbox-Eintrag mit der Thread-ID verlinken: `https://mail.google.com/mail/u/0/#inbox/<thread-id>` (in neuem Tab). Bei anderen Mail-Tools verlinken, wenn eine Web-URL verfügbar ist; sonst ohne Link.
- Optional ausklappbare Antwortvorschläge für Inbox-Einträge.
- News-Links in neuem Tab öffnen.
- Keine externen Skripte.

**Dark Mode via Toggle-Klasse (CSS-Vorlage):**
```css
body.dark { background: #1a1a1a; color: #e0e0e0; }
body.dark .card { background: #2a2a2a; border-color: #3a3a3a; }
body.dark .tag-dringend { background: #5c1a1a; color: #ff9999; }
body.dark .tag-vorbereitung { background: #4a3000; color: #ffcc66; }
body.dark .tag-info { background: #0d2a40; color: #66b3ff; }
body.dark .tag-frei { background: #0d3320; color: #66cc88; }
body.dark .toggle-btn { background: #2a2a2a; border-color: #444; color: #ccc; }
```
Kein `@media (prefers-color-scheme: dark)` verwenden — das Dashboard soll unabhängig vom System-Theme standardmäßig hell erscheinen.

**Schmale Ansicht (Seitenleiste der Desktop-App):**
```css
@media (max-width: 520px) {
  .header { flex-direction: column; gap: 10px; }
  .header-actions { align-self: flex-end; }
  body { padding: 16px 12px; }
  .card { padding: 14px 14px; }
}
```
Den Toggle im Container `.header-actions` platzieren, damit er in der schmalen Ansicht nicht umbricht.

**Mindest-CSS für Lesbarkeit:**
```css
body {
  font-size: 16px;
  line-height: 1.6;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  max-width: 860px;
  margin: 0 auto;
  padding: 24px 16px;
}
.card {
  padding: 16px 20px;
  margin-bottom: 16px;
  border-radius: 8px;
  border: 1px solid #e5e5e5;
}
h2 { font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase; color: #888; margin-bottom: 12px; }
```

---

## Regeln gegen erfundene Inhalte

- Keine erfundenen Termine, Mails, Aufgaben oder News.
- Keine erfundenen Namen, Fristen oder Teilnehmenden.
- Keine News ohne Quelle.
- Bei Unsicherheit klar kennzeichnen: „nicht bekannt", „keine Daten", „nicht verfügbar".

**Keine Diagnose-Texte im Dashboard:** Technische Erklärungen („Datenbank konnte nicht gefiltert werden", „im Label X liegen keine Mails, stattdessen…") gehören in den Chat, nicht in die HTML-Datei. Im Dashboard nur die kurze, nutzerfreundliche Leermeldung zeigen.

**Leere Zustände:**
- Kalender: „Keine festen Termine gefunden."
- Inbox: „Keine Mails mit klarem Handlungsbedarf gefunden."
- Aufgaben: „Keine fälligen Aufgaben gefunden."
- News: Abschnitt weglassen.
- Wetter: Nicht anzeigen, wenn Ort fehlt.

---

## Ton

Warm, direkt und effizient. Wie eine gut gestaltete Arbeitsoberfläche, nicht wie ein langer Bericht.

---

## Herkunft

Dieser Skill wurde für die Community von **KI-Wissen.org** entwickelt — der deutschen Plattform für praxisnahes KI-Wissen. Mehr Tutorials, Skills und Anleitungen findest du unter [ki-wissen.org](https://ki-wissen.org).

---

## Änderungshistorie

**1.0.0** — Erste Veröffentlichung (Juni 2026).
- Tages-Dashboard als einzelne HTML-Datei: Kalender, Aufgaben, Inbox, Wetter, News.
- Einstellungs-Gedächtnis (`Meine Dashboard-Einstellungen/einstellungen.md`) + Onboarding beim ersten Start.
- Funktioniert mit jeder verbundenen Integration (Google, Microsoft, Apple, Notion usw.).
- Dateiname mit Datum + Uhrzeit, automatisches Aufräumen nach 7 Tagen, Abfrage bei vorhandenem Tages-Dashboard.
- Claude öffnet das fertige Dashboard automatisch in voller Breite im Browser (Chrome-Erweiterung); Fallback: Vorschau-Menü ∨ → „In Google Chrome öffnen".
- Hell/Dunkel-Toggle, Abhak-Checkboxen, klickbare Inbox-Einträge, Layout für schmale Seitenleiste.
- Kein „Im Browser öffnen"-Button in der HTML-Datei — die Cowork-Vorschau-Sandbox blockiert jede Navigation (empirisch getestet).
