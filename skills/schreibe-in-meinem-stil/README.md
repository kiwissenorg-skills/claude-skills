# Schreibe in meinem Stil

> Version 1.0.0 · Community · ein Skill von KI-Wissen.org

## Was dieser Skill für dich tut

Schreibt Texte im persönlichen Schreibstil des Nutzers — überarbeitet einen vorhandenen Text in den eigenen Stil oder verfasst einen neuen Text von Grund auf im eigenen Stil. Dabei nutzt der Skill hinterlegte Stilvorlagen (z. B. für Newsletter, Blog, YouTube, LinkedIn) als Zielbild und entfernt gleichzeitig typische Spuren maschinell erzeugter deutscher Texte (Wichtigtuerei, Kanzleisprache, Floskel-Baukasten, Optik-Tells).

## Wann der Skill reagiert

Der Skill löst aus, wenn du z. B. schreibst:
- „Schreibe in meinem Stil" / „in meinem Stil."
- „Mach das wie ich schreibe" / „klingt nach mir."
- „Text humanisieren" / „klingt nach ChatGPT" / „entkünstlichen."
- Oder wenn ein Newsletter, Blogartikel, YouTube-Beschreibung, LinkedIn-Post o. Ä. in deinem Stil geschrieben werden soll.

## Installation

1. `SKILL.md` aus diesem Ordner herunterladen.
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Los — beim ersten Lauf legt der Skill automatisch den leeren Ordner `Meine Schreibstile` an, in den du später eigene Beispieltexte legen kannst.

## Anwendungsbeispiele

**Beispiel 1**
Du: „Mach diesen Newsletter menschlicher: [Text]"
Ergebnis: Der Skill prüft zuerst, ob ein passender hinterlegter Newsletter-Stil existiert, humanisiert den Text in zwei Durchgängen (Aufräumen, Beleben) und liefert im gründlichen Modus zusätzlich einen kurzen Vorher/Nachher-Lerneffekt.

**Beispiel 2**
Du: „Schreib mir einen Blogbeitrag über KI-Automatisierung in meinem Stil." (kein vorhandener Text)
Ergebnis: Der Skill verfasst den Text direkt im hinterlegten Blog-Stilprofil, statt einen vorhandenen Text zu überarbeiten.

## Voraussetzungen

Keine Pflicht-Integration. Eigene Stilvorlagen (empfohlen für beste Ergebnisse) legst du einfach durch das Zuschicken echter eigener Texte an — in beliebigem Format (.docx, .pdf, .txt, .md oder direkt in den Chat kopiert).

## Was ist neu in dieser Version

**v1.0.0** — Erste eigenständige Version „Schreibe in meinem Stil": überarbeitet vorhandene oder verfasst neue Texte im persönlichen Stil, legt beim ersten Lauf automatisch den leeren Ordner `Meine Schreibstile` an (keine Beispielvorlagen werden mitgeliefert), verwaltet mehrere Stile pro Textsorte, Stil-Bestätigung in einem Satz, Vorher/Nachher-Lerneffekt im gründlichen Modus. Details zu den vorausgegangenen internen Iterationen siehe `SKILL.md`-Abschnitt „Änderungshistorie".

## Wenn etwas nicht klappt

- Der Skill fragt nach Tiefe/Ton, obwohl ein Stil hinterlegt ist? → Sollte nicht passieren — bei erkanntem, hinterlegtem Stil fragt der Skill nur, ob dieser Stil verwendet werden soll.
- Kein eigener Stil vorhanden? → Der Skill arbeitet dann nach den allgemeinen Regeln und bietet einmalig an, künftig im eigenen Stil zu schreiben.
- Ergebnis trifft den Ton nicht? → Ein hinterlegter Stil hat immer Vorrang vor den allgemeinen Hinweisen — bei Bedarf die Stilvorlage ergänzen oder präzisieren.

## Herkunft & Lizenz

Die Grundidee — KI-typische Schreibmuster benennen und gezielt entfernen — geht auf den englischsprachigen **„Humanizer"-Skill von blader** ([github.com/blader/humanizer](https://github.com/blader/humanizer)) zurück, der seinerseits auf der Wikipedia-Seite „Signs of AI writing" des WikiProject AI Cleanup basiert. Eigenständig an dieser Fassung sind der Fokus aufs Deutsche (vier Tell-Familien als eigenes Ordnungsraster, deutsche Spezialfälle wie Nominalstil und Kanzleisprache) sowie der persönliche Stilprofil-Mechanismus.

Dieses Projekt steht unter der **Apache License 2.0** (siehe `LICENSE`).

---
Fragen oder Probleme? → https://ki-wissen.org · Ein Skill von KI-Wissen.org (Harald Frey)
