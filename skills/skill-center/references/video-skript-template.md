# Video-Skript-Vorlage

So entsteht das Skript für Haralds Skill-Vorstellungsvideos (YouTube / ki-wissen.org).
Quelle für alle Inhalte: SKILL.md, README.md und CHANGELOG des Skills — **nichts erfinden**,
nur beschreiben, was der Skill nachweislich kann.

## Voraussetzung

Nur für Skills mit Status **freigegeben ✅**. Vorher kein Skript — sonst beschreibt das
Video Funktionen, die sich noch ändern.

## Die 5 Teile (feste Reihenfolge)

**1. Nutzenversprechen (Hook)** — 2–4 Sätze.
Was kann der Zuschauer mit dem Skill tun, mit einem konkreten Alltagsbeispiel.
Muster: „Mit dem <Name>-Skill kannst du … Denn in der Regel hast du ja nicht nur …, sondern …"

**2. Hintergrund / Besonderheit** — 2–4 Sätze.
Was den Skill besonders macht: Herkunft, technischer Kniff in Alltagssprache
(z.B. „deine Vorlagen werden extern gespeichert, damit sie bei einem Update nicht
verloren gehen"). Endet mit dem Scharnier-Satz: **„Wie das funktioniert, zeige ich dir jetzt."**

**3. Installation** — 3–5 Sätze.
Schritte aus der README, inkl. der bekannten Stolperfallen
(Skill per Drag & Drop ins Chatfeld ziehen — nicht übers Plus-Zeichen; „Save skill"-Button;
falls kein Button erscheint: „bitte abspeichern" eingeben; neue Session nach Installation).

**4. Demo-Durchlauf** — Hauptteil.
Die 2–3 wichtigsten Anwendungsfälle aus den README-Beispielen, als Bildschirm-Erzählung:
Was Harald eingibt („Dann gibst du … ein"), was Claude daraufhin tut, was der Zuschauer
sieht. Implizite Regieanweisungen im Fließtext („Hier kopiere ich einfach einen Text
hinein …"). Wiederkehrende Voraussetzungen (z.B. „der Ordner muss zugeordnet sein")
bei jedem Anwendungsfall kurz wiederholen — Zuschauer springen im Video.

**5. Zusammenfassung** — 1 Satz.
Muster: „So kann ich mit einem einzigen Skill … verwalten, einsetzen und optimieren."

## Stilmerkmale (aus Haralds Mustertext)

- **Du-Ansprache** durchgehend; bei eigenen Demo-Handlungen „ich" („Hier kopiere ich …").
- **Präsens**, kurze Hauptsätze, keine Schachtelsätze.
- Kein Fachjargon; wo nötig in einem Halbsatz erklären („im MD-Format, sodass die KI
  sie später gut lesen kann").
- Fließtext ohne Bullet-Points — das Skript wird gesprochen, nicht gelesen.
- Ehrlich bleiben: Einschränkungen benennen wie im Muster („über das Plus-Zeichen
  lässt er sich leider nicht direkt hochladen").

## Ablauf

1. Status prüfen (freigegeben ✅). Wenn nicht → Hinweis, abbrechen.
2. SKILL.md, README, CHANGELOG des Skills lesen.
3. Skript nach den 5 Teilen entwerfen, Länge ca. 350–550 Wörter (≈ 3–4 Minuten Sprechzeit).
4. Speichern als `Skills/<skill-name>/video-skript-v<version>.md` — versioniert,
   damit Skript und Skill-Version zusammenpassen.
5. Harald das Skript zeigen. Für Teleprompter-Optimierung und docx-Export auf die
   bestehenden Skills `youtube-skript` bzw. `ki-videotutorials` verweisen —
   deren Logik hier NICHT duplizieren.
6. Im REGISTER vermerken: „Video-Skript v<version> erstellt am <Datum>".
