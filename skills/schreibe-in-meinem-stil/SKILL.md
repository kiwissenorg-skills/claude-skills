---
name: schreibe-in-meinem-stil
version: 1.0.0
description: Schreibt Texte im persönlichen Schreibstil des Nutzers — überarbeitet einen vorhandenen Text in den eigenen Stil oder verfasst einen neuen Text von Grund auf im eigenen Stil. Nutzt hinterlegte Stilvorlagen (Newsletter, Blog, YouTube, LinkedIn u.a.) als Zielbild und entfernt zugleich typische Spuren deutscher KI-Texte. Aktivieren bei: "schreibe in meinem Stil", "in meinem Stil", "mach das wie ich schreibe", "klingt nach mir", sowie weiterhin "natürlich schreiben", "Text humanisieren", "klingt nach ChatGPT", "KI-Text entschärfen", "entkünstlichen", "zu glatt", "zu formell", "menschlicher machen" — oder wenn ein Text (Newsletter, Blog, YouTube-Beschreibung, LinkedIn-Post, Kurstext) im eigenen Stil geschrieben oder weniger nach Maschine klingen soll.
---

# Schreibe in meinem Stil

Ein Skill von **KI-Wissen.org** für die Community.

Maschinell erzeugte deutsche Texte haben einen Klang. Man hört ihn nicht an einem einzelnen Wort, sondern an einem Bündel von Gewohnheiten, die Sprachmodelle immer wieder zeigen: aufgeblasene Wichtigkeit, Verwaltungsdeutsch, Floskeln, die nach Beratung klingen, und ein Satzbau, der zu gleichmäßig ist, um von einem Menschen zu stammen. Dieser Skill bringt einen Text zurück in eine Form, die jemand wirklich geschrieben haben könnte.

Wichtig vorweg: Das Ziel ist nicht, Wörter gegen Synonyme zu tauschen. Das Ziel ist, dem Text Haltung, Rhythmus und ein paar menschliche Kanten zurückzugeben. Ein technisch „sauberer", aber seelenloser Text klingt genauso nach Maschine wie ein floskelhafter.

---

## Zwei Betriebsarten: Überarbeiten oder neu schreiben

Dieser Skill kann zwei Dinge:

1. **Vorhandenen Text in meinen Stil bringen** (Standard). Der Nutzer liefert einen Text — oft KI-generiert oder zu glatt — und der Skill humanisiert ihn und gleicht ihn an den hinterlegten Stil an. Auslöser z.B. „mach das in meinem Stil", „das klingt nach KI".

2. **Neuen Text im eigenen Stil verfassen.** Liefert der Nutzer keinen fertigen Text, sondern nur ein Thema, Stichpunkte oder einen Auftrag („schreib mir einen Newsletter über X in meinem Stil"), dann den Text **von Grund auf** schreiben — direkt nach dem hinterlegten Stilprofil der passenden Textsorte. Hier gibt es keinen „Durchgang 1 Aufräumen", weil nichts aufzuräumen ist; stattdessen den Text gleich so verfassen, dass er die Stilmerkmale trägt (Ansprache, Satzrhythmus, typische Wendungen) und keine KI-Tells enthält. Anschließend denselben Selbstcheck wie beim gründlichen Modus anwenden.

Welche Betriebsart gemeint ist, ergibt sich meist aus dem Auftrag: Gibt es einen vorhandenen Fließtext zum Überarbeiten → Betriebsart 1. Gibt es nur Thema/Stichpunkte → Betriebsart 2. Im Zweifel kurz nachfragen. In **beiden** Betriebsarten gilt der Stil-Vorrang und das Vorgehen zum Stilladen unten.

---

## So läuft die Überarbeitung ab

Zuerst den **Stil** prüfen (Durchgang 0), dann — nur falls nötig — den Modus klären (siehe unten), dann den Text in zwei Durchgängen bearbeiten:

**Durchgang 0 — Stil laden (zuerst, nicht optional überspringen).** Als allererstes prüfen, ob im Ordner `Meine Schreibstile` eine zur Textsorte passende, gefüllte `stil-<name>.md` liegt, und daraus das Stilprofil ableiten (siehe Abschnitt „Eigenen Stil als Zielbild nutzen"). Das Ergebnis dieses Durchgangs entscheidet, ob überhaupt nach Tiefe/Ton gefragt wird.

**Durchgang 1 — Aufräumen.** Den Text gegen die vier Tell-Familien prüfen (Wichtigtuerei, Kanzleisprache, Floskel-Baukasten, Optik) und jede auffällige Stelle umformulieren. Bedeutung und Fachinhalt bleiben unangetastet.

**Durchgang 2 — Beleben.** Den aufgeräumten Text laut durchgehen und fragen: Hat hier jemand etwas gemeint, oder läuft ein Generator? Rhythmus brechen, eine Haltung einziehen, wo es passt, und konkret werden, wo der Text vage bleibt.

Beim gründlichen Modus folgt am Ende noch ein ehrlicher Selbstcheck („Was riecht hier noch nach KI?") und eine zweite, geschliffene Fassung.

---

## Erst den Stil klären, dann den Modus

**Reihenfolge ist wichtig:** Bevor irgendeine Frage zu Tiefe oder Ton kommt, zuerst den Stilvorlagen-Ordner prüfen (Durchgang 0) und die Textsorte aus dem Auftrag ableiten. Erst danach entscheiden, was überhaupt gefragt werden muss.

**Fall A — passender Stil vorhanden (Normalfall).** Lässt sich die Textsorte erkennen (z.B. Newsletter) und es gibt dafür eine gefüllte `stil-<name>.md`, dann **nicht** nach Tiefe und Ton fragen. Stattdessen mit `AskUserQuestion` genau eine Frage stellen:

> „Möchtest du deinen hinterlegten **<Textsorte>**-Schreibstil verwenden?" — Optionen: **Ja, meinen Stil verwenden** / **Nein, neutral humanisieren**.

Sagt der Nutzer Ja, den hinterlegten Stil als Zielbild nehmen. In beiden Fällen gilt voreingestellt: **Tiefe = gründlich** (Selbstcheck plus zweite Fassung) und **Ton = aus dem hinterlegten Stil übernommen** (bei „Nein" sachlich-neutral). Diese Defaults nicht extra erfragen — der Nutzer wollte ausdrücklich weniger Fragerei.

**Fall B — kein passender Stil (kein Stilordner, nur leere Vorlagen, oder Textsorte unklar bei mehreren Stilen).** Erst die Stilauswahl klären (siehe „So wählt der Skill den richtigen Stil"). Nur wenn gar kein Stil greift, mit `AskUserQuestion` kurz nach dem Modus fragen, falls der Auftrag ihn nicht vorgibt:

- **Wie tief?** Schneller Durchgang (offensichtliche Tells raus, eine Fassung) oder gründlich (Selbstcheck plus zweite Fassung).
- **Welcher Ton?** Sachlich bleiben (nur entkünsteln) oder persönlicher werden (mehr Haltung, lockerer, für Newsletter/YouTube/LinkedIn).

**Immer ohne Rückfrage loslegen** bei ein, zwei Sätzen, eindeutigem Auftrag, oder wenn der Nutzer Stil/Modus schon genannt hat.

---

## Eigenen Stil als Zielbild nutzen (optional, aber stark)

Ein humanisierter Text wirkt erst dann wirklich überzeugend, wenn er nach einer bestimmten Person klingt — und nicht nach „irgendeinem Menschen". Dieser Skill kann den persönlichen Schreibstil des Nutzers als Vorlage lernen. Und weil derselbe Mensch je nach Textsorte unterschiedlich schreibt (ein Newsletter klingt anders als ein Blogartikel oder eine YouTube-Beschreibung), kann der Skill **mehrere Stile** verwalten und den passenden auswählen.

### Wo die Stilvorlagen liegen (update-sicher)

Damit ein Update des Skills die persönlichen Stilvorlagen nicht überschreibt, liegen diese **außerhalb** des Skills — in einem Ordner mit dem festen Namen **`Meine Schreibstile`**, der in einem der verbundenen Cowork-Ordner des Nutzers liegt. So bleibt der Skill austauschbar, ohne dass jemand seine Vorlagen verliert. Der Name ist bewusst benutzerunabhängig: Der Skill sucht nach dem Ordnernamen, nicht nach einem festen Pfad — dieselbe Anweisung funktioniert deshalb bei jedem Nutzer.

Jede Datei in diesem Ordner steht für einen Stil und ist nach dem Muster `stil-<name>.md` benannt, zum Beispiel `stil-newsletter.md`, `stil-blog.md`, `stil-youtube.md`. In jeder Datei stehen ein bis drei echte Beispieltexte dieser Sorte. Leere Dateien und reine Platzhalter werden übersprungen.

**So findet der Skill den Ordner:** In den verbundenen Cowork-Ordnern nach einem Ordner namens `Meine Schreibstile` suchen und dessen gefüllte `stil-*`-Dateien verwenden. Hat der Nutzer einmal einen abweichenden Ort genannt, diesen merken und bevorzugt verwenden.

**Ordner ja, Vorlagen nein — der wichtige Unterschied.** Beim ersten Lauf (erste Texteingabe) prüft der Skill, ob ein Ordner `Meine Schreibstile` existiert. Fehlt er, legt der Skill **den leeren Ordner automatisch an** — als Briefkasten, in den der Nutzer später eigene Vorlagen legen kann. In den Ordner kommt dabei **nur** eine kurze `Liesmich.md` mit einer Anleitung. Der Skill legt **keine** `stil-*.md`-Vorlagen an und liefert auch keine Beispielvorlagen mit; `stil-*.md`-Dateien entstehen ausschließlich später aus echten Texten, die der Nutzer selbst liefert.

**Wo anlegen:** In einem verbundenen Cowork-Ordner. Gibt es mehrere, **einmal kurz nachfragen**, in welchem der Ordner angelegt werden soll. Ist gar kein Ordner mit Cowork verbunden, kann der Skill keinen anlegen — dann einmal darauf hinweisen und den Text trotzdem nach den allgemeinen Regeln bearbeiten. Hat der Nutzer einmal einen abweichenden Ort genannt, diesen merken und bevorzugt verwenden.

**Nach dem Anlegen** kurz Bescheid geben und konkret anleiten: „Ich habe den (leeren) Ordner `Meine Schreibstile` angelegt. Wenn du möchtest, dass ich in deinem Stil schreibe, schick mir 1–3 echte Texte von dir (z.B. Newsletter, Blog) oder lade sie als Datei hoch — ich lege sie dann als Vorlage ab. Solange der Ordner leer ist, schreibe ich nach den allgemeinen Regeln."

**Inhalt der `Liesmich.md`** (beim Anlegen hineinschreiben):
> # Meine Schreibstile
> Lege hier deine persönlichen Schreibstil-Vorlagen ab, damit der Skill „Schreibe in meinem Stil" in deinem Ton schreibt.
> - Pro Textsorte eine Datei nach dem Muster `stil-<name>.md`, z.B. `stil-newsletter.md`, `stil-blog.md`.
> - In jede Datei 1–3 echte Texte von dir (keine KI-Texte), ein paar Absätze genügen.
> - Du kannst die Texte auch einfach im Chat hereinkopieren oder hochladen — der Skill legt die passende Datei dann selbst an.
> - Diese `Liesmich.md` wird vom Skill ignoriert; sie dient nur dir als Anleitung.

### So wählt der Skill den richtigen Stil

1. **Stilordner bestimmen.** In den verbundenen Cowork-Ordnern nach dem Ordner `Meine Schreibstile` suchen und ihn verwenden, falls vorhanden. Fehlt er, beim ersten Lauf den **leeren** Ordner automatisch anlegen (nur mit `Liesmich.md`, keine `stil-*.md`-Vorlagen) und nach den allgemeinen Regeln arbeiten.
2. **Vorhandene Stile ermitteln.** Den Ordner durchsehen und alle gefüllten `stil-*`-Dateien als verfügbare Stile auflisten.
3. **Aus dem Auftrag ableiten.** Geht aus der Anfrage klar hervor, um welche Textsorte es geht (z.B. „mach diesen Newsletter menschlicher" → `stil-newsletter`, „das ist ein Blogartikel" → `stil-blog`), automatisch den passenden Stil nehmen, ohne zu fragen.
4. **Bei Unklarheit fragen.** Lässt sich die Textsorte nicht eindeutig zuordnen und es gibt mehrere Stile, kurz mit `AskUserQuestion` nachfragen: „In welchem Stil soll ich schreiben?" — die vorhandenen Stile zur Auswahl anbieten, plus die Option „kein bestimmter Stil".
5. **Nur ein Stil vorhanden.** Gibt es nur eine gefüllte Stildatei, diese direkt verwenden, ohne zu fragen.
6. **Keine eigenen Stile vorhanden (Ordner fehlt oder enthält nur die `Liesmich.md`).** Fehlt der Ordner, ihn beim ersten Lauf leer anlegen (siehe oben). Den Text nach den allgemeinen Regeln bearbeiten und am Ende **einmal** kurz anbieten: „Wenn du möchtest, kann ich künftig in deinem eigenen Stil schreiben — schick mir dazu einfach 1–3 echte Texte von dir (Newsletter, Blog o.Ä.), dann lege ich sie als Vorlage ab." **Stil-Vorlagen** (`stil-*.md`) nur mit echten, vom Nutzer gelieferten Texten anlegen — niemals leere oder erfundene.

### Neue Stilvorlage hinzufügen (Format egal)

Wenn der Nutzer eine Stilvorlage hinzufügen will (z.B. „speicher das als Vorlage für Blogbeiträge", „nimm das als Newsletter-Stil"), gilt: **Das Eingabeformat ist egal** — der Nutzer darf `.docx`, `.txt`, `.pdf`, `.md` oder einfach reinkopierten Text liefern. Der Skill speichert die Vorlage aber **immer als `.md`** im Stilvorlagen-Ordner, mit korrektem Namen. Vorgehen:

1. **Text extrahieren.** Aus der hochgeladenen Datei den reinen Text gewinnen — bei `.docx`/`.pdf` z.B. mit `pandoc` oder den entsprechenden Bordmitteln, bei `.txt`/`.md` direkt übernehmen. Reiner Fließtext genügt; Formatierung, Bilder und Tabellen sind für einen Schreibstil irrelevant.
2. **Textsorte bestimmen.** Aus dem Auftrag ableiten, um welchen Stil es geht (Blog, Newsletter, …). Ist es unklar, kurz nachfragen.
3. **Als `stil-<name>.md` ablegen.** Den extrahierten Text in eine Datei `stil-<textsorte>.md` im Stilvorlagen-Ordner schreiben, z.B. `stil-blog.md`. Existiert die Datei schon und ist gefüllt, nachfragen, ob ergänzen oder ersetzen.
4. **Bestätigen.** Kurz melden, unter welchem Stilnamen die Vorlage gespeichert wurde, z.B. „Gespeichert als Blog-Stil (`stil-blog.md`)."

Die `.docx`- oder `.pdf`-Originaldatei selbst gehört **nicht** unverändert in den Stilvorlagen-Ordner — dort liegen nur die umgewandelten `.md`-Dateien, damit das Lesen einheitlich funktioniert.

### Was aus der Vorlage übernommen wird

Aus der gewählten Stildatei ein kurzes Stilprofil ableiten: typische Satzlänge und Rhythmus, Ansprache (du/Sie/wir), Lieblingswörter und -wendungen, Grad an Lockerheit oder Sachlichkeit, Humor, wie Beispiele eingeführt werden, wie Absätze beginnen und enden. Nur die **Form** übernehmen — niemals Inhalte oder Aussagen aus den Vorlagen in den bearbeiteten Text mischen. Ziel ist nicht, einen Vorlagentext zu imitieren, sondern den zu humanisierenden Text so klingen zu lassen, als hätte ihn dieselbe Person in derselben Textsorte geschrieben.

**Stil kurz bestätigen.** Sobald das Stilprofil abgeleitet ist, dem Nutzer in **einem** Satz zeigen, welcher Stil erkannt wurde, bevor losgelegt wird — z.B. „Erkannt: Newsletter-Stil — du-Form, warm, kurze Sätze, persönlicher Gruß." So sieht der Nutzer sofort, ob der richtige Stil greift. Kein langer Bericht, nur der Einzeiler.

**Wichtig:** Ein hinterlegter Stil hat Vorrang vor den allgemeinen „Was Stimme ausmacht"-Hinweisen, wo beide sich widersprechen. Ist der Newsletter-Stil z.B. förmlich und siezend, dann nicht eigenmächtig auf lockeres Du umstellen.

---

## Die vier Tell-Familien

Statt einer langen Einzelliste lohnt es sich, die Muster in vier Gruppen zu denken. Wer diese vier Familien kennt, erkennt fast jeden KI-Text.

### Familie A — Wichtigtuerei

Modelle blähen Bedeutung auf. Aus einem normalen Sachverhalt wird eine historische Weichenstellung, aus einem Tool eine Revolution.

**Bedeutungs-Inflation.** „spielt eine entscheidende/zentrale Rolle", „markiert einen Meilenstein", „einen wesentlichen Beitrag leisten", „wegweisend", „bahnbrechend", „prägend". Alles bekommt Weltgewicht.

> *Vorher:* Die Veröffentlichung dieses Prompts markiert einen wichtigen Meilenstein und spielt eine zentrale Rolle dabei, KI für alle zugänglich zu machen.
> *Nachher:* Diesen Prompt kannst du sofort übernehmen — er spart dir bei jeder Recherche ein paar Minuten.

**Werbe- und Tool-Lyrik.** „besticht durch", „verzaubert", „atemberaubend", „revolutionär", „ein absolutes Muss", „einzigartig", „erstklassig". Besonders dick bei Tool-Vorstellungen.

> *Vorher:* Dieses revolutionäre Tool besticht durch seine einzigartige Oberfläche und verzaubert mit einer atemberaubenden Funktionsvielfalt.
> *Nachher:* Die Oberfläche ist aufgeräumt. Stark ist vor allem die Transkription — ein langes Video ist in unter einer Minute fertig.

**Kopula-Flucht.** Statt eines schlichten „ist" greift die KI zu „stellt dar", „fungiert als", „dient als", „bildet die Grundlage", „verkörpert". Klingt gewichtig, ist aber leer.

> *Vorher:* Der Kurs stellt eine wertvolle Möglichkeit dar und fungiert als solide Grundlage für den Einstieg.
> *Nachher:* Der Kurs ist für Einsteiger. Vorkenntnisse brauchst du keine.

**Vage Autoritäten.** „Studien zeigen", „Expertinnen und Experten zufolge", „in Fachkreisen gilt", „Beobachter weisen darauf hin" — nie mit konkreter Quelle.

> *Vorher:* Studien zeigen, dass Experten von einem erheblichen Produktivitätsgewinn durch KI ausgehen.
> *Nachher:* Eine Stanford-Studie von 2023 (Bloom et al.) fand bei Remote-Arbeit eine um 13 % höhere Produktivität.

---

### Familie B — Kanzleisprache

Das vielleicht deutscheste KI-Problem. Modelle schreiben Deutsch gern wie ein Amt: viele Substantive, schwache Verben, unpersönliche Konstruktionen.

**Nominalstil-Stau.** Hohe Dichte an -ung/-heit/-keit/-tion plus Blassverben (erfolgen, durchführen, gewährleisten, stattfinden).

> *Vorher:* Die Durchführung einer Optimierung erfolgt unter Berücksichtigung der Anforderungen zur Gewährleistung einer erfolgreichen Umsetzung.
> *Nachher:* Wir optimieren die Prozesse und achten dabei darauf, was wirklich gebraucht wird.

**Verwaltungs-Übergänge.** „Es lässt sich festhalten, dass", „Zusammenfassend lässt sich sagen", „An dieser Stelle sei erwähnt", „Im Folgenden wird dargelegt". So redet kein Mensch.

> *Vorher:* Zusammenfassend lässt sich festhalten, dass KI-Tools im Arbeitsalltag erhebliche Potenziale bergen.
> *Nachher:* Unterm Strich sparen KI-Tools im Alltag echt Zeit — wenn du weißt, wofür sie taugen.

**Partizip-Anhängsel.** Der Hauptsatz endet, dann kommt ein Partizip-I-Schwanz: „…unterstreichend", „…verdeutlichend", „…widerspiegelnd". Aus dem englischen „-ing" geklaut, im Deutschen doppelt steif.

> *Vorher:* Das Tutorial deckt die Grundlagen ab, die Bedeutung guter Prompts unterstreichend.
> *Nachher:* Das Tutorial deckt die Grundlagen ab. Den größten Unterschied macht, wie gut dein Prompt formuliert ist.

---

### Familie C — Der Floskel-Baukasten

Fertigteile, die in fast jedem KI-Text auftauchen, weil sie statistisch „seriös" wirken.

**Hohle Einstiege.** „In der heutigen schnelllebigen Welt…", „Im digitalen Zeitalter…", „KI ist in aller Munde…", „KI verändert die Welt, wie wir sie kennen…". Gerade im KI-Thema komplett abgenutzt.

> *Vorher:* In der heutigen schnelllebigen Welt, in der KI in aller Munde ist, wird gutes Prompten immer wichtiger.
> *Nachher:* Ob ein KI-Ergebnis brauchbar ist, hängt fast immer am Prompt.

**Beratersprech.** „aufs nächste Level heben", „das volle Potenzial ausschöpfen", „den entscheidenden Unterschied machen", „ganzheitlicher Ansatz", „maßgeschneiderte Lösung", „Game Changer", „Deep Dive". Sagt nichts.

> *Vorher:* Mit unserem ganzheitlichen Ansatz heben wir dein Business aufs nächste Level.
> *Nachher:* Wir schauen uns deine Abläufe an und zeigen dir, wo Zeit liegen bleibt.

**Lieblingswörter im Rudel.** zudem, darüber hinaus, des Weiteren, insbesondere, maßgeblich, umfassend, ganzheitlich, facettenreich, nahtlos, leistungsstark, innovativ, Synergie, Mehrwert. Drei davon im selben Absatz = klare KI-Signatur.

> *Vorher:* Zudem bietet die Plattform eine umfassende, nahtlose Integration und liefert insbesondere durch ihren innovativen Ansatz echten Mehrwert.
> *Nachher:* Die Plattform hängt sich ohne Umwege an bestehende Systeme an. Neu ist die automatische Konfliktauflösung beim Datenabgleich.

**Die Dreier-Schablone.** Alles kommt in Gruppen von drei, oft sind alle drei Begriffe dasselbe.

> *Vorher:* Das Tool ist schnell, einfach und effizient — für Klarheit, Struktur und Übersicht.
> *Nachher:* Das Tool ist schnell. Die Bedienung hast du in zehn Minuten raus.

**Das „nicht nur, sondern auch"-Pärchen.** „Es geht nicht nur um X, sondern auch um Y", „weniger X, mehr Y", „keine Frage des Ob, sondern des Wann".

> *Vorher:* Es geht nicht nur um die Technik, sondern auch um die Kultur im Team.
> *Nachher:* Technisch ist das lösbar. Schwerer wird's, die Leute mitzunehmen.

**Synonym-Karussell.** Aus Angst vor Wiederholung heißt dieselbe Sache in vier Sätzen „der Protagonist", „der Held", „die zentrale Figur", „der Hauptakteur".

> *Vorher:* Die Protagonistin steht vor Herausforderungen. Die Heldin überwindet Hindernisse. Die zentrale Figur triumphiert.
> *Nachher:* Die Protagonistin steht vor einigen Hürden, kommt aber durch.

**Scheinbare Spannweiten.** „von X bis Y", wo X und Y gar nicht auf einer Skala liegen.

> *Vorher:* Die Reise führt vom Urknall bis zur dunklen Materie, vom ersten Stern bis zum kosmischen Netz.
> *Nachher:* Das Buch behandelt den Urknall, die Sternentstehung und aktuelle Theorien zur dunklen Materie.

**Hedging und Optimismus-Schluss.** Dreifach abgesichert („könnte unter Umständen möglicherweise") und am Ende ein Sonnenaufgang („Die Zukunft sieht vielversprechend aus").

> *Vorher:* Es könnte potenziell argumentiert werden, dass die Maßnahme einen gewissen Einfluss haben könnte. Die Zukunft sieht vielversprechend aus.
> *Nachher:* Die Maßnahme dürfte etwas bringen. Nächstes Jahr kommen zwei weitere Standorte dazu.

---

### Familie D — Die Optik

Tells, die man schon sieht, bevor man liest.

**Gedankenstrich-Flut.** Halbgeviert- (–) und Geviertstriche (—) gehäuft, um „pointiert" zu wirken.

> *Vorher:* Der Begriff wird von Institutionen geprägt – nicht von den Betroffenen – und hält sich trotzdem – sogar in Dokumenten.
> *Nachher:* Der Begriff wird von Institutionen geprägt, nicht von den Betroffenen, und hält sich trotzdem sogar in offiziellen Dokumenten.

**Fett-Inflation und Label-Bullets.** Mechanisch gefettete Schlüsselwörter; Listen, in denen jeder Punkt mit fettem Wort und Doppelpunkt anfängt, obwohl Fließtext besser wäre.

> *Vorher:*
> - **Oberfläche:** Die Oberfläche wurde überarbeitet.
> - **Tempo:** Das Tempo wurde gesteigert.
>
> *Nachher:* Die Oberfläche ist neu und lädt spürbar schneller.

**Emoji-Deko.** 🚀 💡 ✅ vor jeder Zeile. (Bei YouTube-Beschreibungen sind einzelne, gezielte Emojis oft gewollt — verdächtig ist erst die mechanische Dekoration jeder Zeile.)

**Anführungszeichen-Mix.** „…", "…" und »…« wild gemischt. Für deutschen Fließtext „…" oder »…«, in Code "gerade" — Hauptsache konsistent.

---

## Was Stimme ausmacht (Durchgang 2)

Ein Text kann alle vier Familien sauber vermeiden und trotzdem leblos sein. Daran erkennt man das:

- Alle Sätze etwa gleich lang und gleich gebaut.
- Reines Referieren ohne jede Haltung.
- Keine Ambivalenz, kein Zweifel, kein „ich weiß auch nicht recht".
- Keine Ich- oder Du-Form, wo sie natürlich wäre.
- Liest sich wie ein Lexikoneintrag, obwohl es keiner sein soll.

Gegenmittel:

**Rhythmus brechen.** Kurzer Satz. Dann einer, der sich mehr Zeit nimmt und ruhig ein paar Nebengedanken mitnimmt. Wechsel erzeugt Leben.

**Haltung zeigen.** Nicht nur berichten — reagieren. „Mich überzeugt das noch nicht ganz" ist menschlicher als eine ausgewogene Aufzählung.

**Konkret statt abstrakt.** Nicht „das ist besorgniserregend", sondern „es ist schon eigenartig, dass die Modelle nachts durchlaufen und keiner hinschaut".

**Direkt ansprechen.** Bei Newsletter, Tutorial, Social: Du-Form ist meist natürlicher als die distanzierte dritte Person.

**Unordnung erlauben.** Eine Klammer, eine Abschweifung, ein halb ausgesprochener Gedanke. Perfektion wirkt algorithmisch.

---

## Ausgabe

**Schneller Modus:** eine überarbeitete Fassung, optional ein paar Stichpunkte zu den wichtigsten Änderungen.

**Gründlicher Modus:**
1. Erste Überarbeitung
2. „Was riecht hier noch nach KI?" — knappe Stichpunkte
3. Zweite, geschliffene Fassung
4. **Vorher/Nachher (Lerneffekt).** Am Ende die 3–5 stärksten Änderungen kurz benennen — jeweils was KI-typisch war und wie es jetzt klingt, z.B. „‚In der heutigen Welt' → konkreter Einstieg" oder „Nominalstil ‚Durchführung der Prüfung' → ‚wir prüfen'". So sieht der Nutzer, woran man den KI-Klang erkennt, und lernt mit. Knapp halten, kein Roman.

---

## Durchgespieltes Beispiel

**Ausgangstext (typischer KI-Blogeinstieg):**
> Gerne! Hier ist dein Text. Ich hoffe, das hilft!
>
> In der heutigen schnelllebigen Welt, in der KI in aller Munde ist, stellt KI-gestütztes Schreiben einen Meilenstein dar und spielt eine zunehmend entscheidende Rolle. Diese wegweisenden Tools — eingebettet in eine sich rasant wandelnde Landschaft — prägen unsere Arbeit nachhaltig.
>
> Im Kern geht es nicht nur um Effizienz, sondern auch um Kreativität. Die Tools fungieren als Partner. Die Systeme bilden die Grundlage für Innovation.
>
> - 💡 **Tempo:** Texte entstehen schneller.
> - 🚀 **Qualität:** Die Qualität steigt.
>
> Zusammenfassend lässt sich festhalten: Die Zukunft sieht vielversprechend aus. Lass mich wissen, wenn ich etwas vertiefen soll!

**Was riecht hier nach KI?**
- Chatrahmen („Gerne!", „Lass mich wissen…")
- Hohler Einstieg + Bedeutungs-Inflation („Meilenstein", „entscheidende Rolle", „wegweisend")
- Kopula-Flucht („fungieren als", „bilden die Grundlage")
- „nicht nur, sondern auch", Label-Bullets, Emojis
- Verwaltungs-Fazit + Optimismus-Schluss

**Überarbeitet:**
> KI-Tools machen dich beim Schreiben schneller — vor allem bei den langweiligen Teilen. Bei den eigentlichen Ideen weniger.
>
> Stark sind sie bei Rohfassungen, Gliederungen, dem zwanzigsten Variantentitel. Schwach sind sie darin, zu merken, wann sie danebenliegen. Ich hab schon Absätze übernommen, die flüssig klangen und trotzdem am Punkt vorbei gingen — einfach weil ich aufgehört hatte, genau zu lesen.
>
> Mein Rat: Nutz die Tools für den ersten Wurf, aber schreib den Schluss selbst. Der Schluss ist die Stelle, an der man am deutlichsten hört, ob da ein Mensch war.

**Geändert:** Chatrahmen raus, Bedeutungs-Inflation und Werbelyrik raus, Kopula-Flucht aufgelöst, „nicht nur/sondern auch" weg, Bullets und Emojis zu Fließtext, Verwaltungs-Fazit und Optimismus-Schluss ersetzt, Du-Form und variabler Rhythmus rein.

---

## Herkunft

Dieser Skill wurde für die Community von **KI-Wissen.org** entwickelt. Die Grundidee — KI-typische Schreibmuster benennen und gezielt entfernen — geht auf den englischsprachigen **„Humanizer"-Skill von blader** (https://github.com/blader/humanizer) zurück, der seinerseits auf der Wikipedia-Seite „Signs of AI writing" des WikiProject AI Cleanup basiert.

Eigenständig an dieser Fassung ist der Fokus aufs Deutsche: die vier Tell-Familien als eigenes Ordnungsraster, die deutschen Spezialfälle (Nominalstil, Kanzleisprache, Beratersprech, hohle KI-Einstiege) und Beispiele aus der Praxis von KI-Wissen.org. Die englischen Tells werden bewusst nicht eins zu eins übernommen, weil deutsche Modelle anders danebengreifen.

---

## Änderungshistorie

**1.0.0** — Erste eigenständige Version „Schreibe in meinem Stil" (Aufbauphase).
- Skill schreibt Texte im persönlichen Stil des Nutzers — überarbeitet vorhandene oder verfasst neue Texte.
- **Legt KEINE `stil-*.md`-Vorlagen selbst an** und liefert keine Beispielvorlagen mit. Ohne eigene Stile gelten die allgemeinen Regeln.
- Legt beim ersten Lauf automatisch den **leeren Ordner `Meine Schreibstile`** (nur mit Anleitungs-`Liesmich.md`) an, damit der Nutzer dort später eigene Vorlagen ablegen kann. Bei mehreren verbundenen Ordnern wird einmal nachgefragt.
- Eigene Stile jederzeit möglich: Der Nutzer schickt echte Texte, der Skill legt sie auf Wunsch als `stil-<name>.md` im Ordner `Meine Schreibstile` ab.
- Auslöser u.a. „schreibe in meinem Stil", „in meinem Stil", „klingt nach mir" sowie die bisherigen Humanisieren-Phrasen.
- Stil zuerst, weniger Fragerei; Stil-Bestätigung in einem Satz; Vorher/Nachher im gründlichen Modus.

<details>
<summary>Frühere interne Iterationen (vor der 1.0.0-Veröffentlichung)</summary>

**2.0.0** — „Schreibe in meinem Stil".
- Skill umbenannt; Auslöser jetzt auch „schreibe in meinem Stil", „in meinem Stil", „klingt nach mir" (Humanisieren-Auslöser bleiben erhalten).
- Neue Betriebsart: Texte auf Wunsch von Grund auf im eigenen Stil verfassen, nicht nur vorhandene überarbeiten.
- Konkreter Onboarding-Hinweis (Schritt für Schritt), wie man Beispieltexte hinterlegt.
- Stil-Bestätigung in einem Satz, bevor losgelegt wird.
- Gründlicher Modus zeigt jetzt 3–5 Vorher/Nachher-Änderungen als Lerneffekt.

**1.2.0** — Stil zuerst, weniger Fragerei.
- Bei erkannter Textsorte mit hinterlegtem Stil fragt der Skill jetzt zuerst „Möchtest du deinen hinterlegten <Textsorte>-Stil verwenden?" — statt generisch nach Tiefe und Ton.
- Tiefe (gründlich) und Ton (aus dem Stil) werden als sinnvolle Defaults angenommen und nicht mehr extra erfragt.
- Die Modusfragen (Tiefe/Ton) kommen nur noch, wenn gar kein Stil greift.

**1.1.0** — Komfort bei den Stilvorlagen.
- Stilvorlagen dürfen in jedem Format hochgeladen werden (.docx, .pdf, .txt, .md oder reinkopierter Text); der Skill wandelt sie automatisch in `stil-<name>.md` um.
- Hinweis: In Version 1.0.0 legt der Skill bewusst KEINE Stilvorlagen mehr selbst an (siehe 1.0.0).

**1.0.0** — Erste öffentliche Fassung für die Community.
- Vier Tell-Familien (Wichtigtuerei, Kanzleisprache, Floskel-Baukasten, Optik) mit deutschen Beispielen
- Zwei Bearbeitungsmodi (schnell / gründlich) und Tonwahl (sachlich / lockerer)
- Persönlicher Schreibstil als Zielbild, mit mehreren Stilen pro Textsorte
- Stilvorlagen update-sicher in einem externen Ordner (gehen bei Skill-Updates nicht verloren)
- Offener Herkunftshinweis auf den „Humanizer" von blader

*Hinweis fürs Aktualisieren: Bei neuen Versionen die Nummer oben im `version`-Feld erhöhen und hier einen kurzen Eintrag ergänzen. Schema HAUPT.NEBEN.PATCH — Hauptzahl für große Umbauten, mittlere für neue Funktionen, letzte für Korrekturen.*

</details>
