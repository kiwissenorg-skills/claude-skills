# Morgen-Dashboard

> Version 1.0.0 · Community · ein Skill von KI-Wissen.org

## Was dieser Skill für dich tut

Erstellt ein ruhiges, übersichtliches Tages-Dashboard als einzelne HTML-Datei — mit den wichtigsten Informationen aus Kalender, E-Mail-Postfach und Aufgaben, optional ergänzt um Wetter und News. Ziel ist nicht, möglichst viele Informationen zu zeigen, sondern die wichtigsten Entscheidungen für den Tag sichtbar zu machen. Das Dashboard lässt sich auch als volle Browserseite öffnen.

## Wann der Skill reagiert

Der Skill löst aus, wenn du z. B. schreibst:
- „Mach mir ein Morgen-Dashboard."
- „Tages-Dashboard für heute."
- „Zeig mir mein Dashboard."
- „Was liegt heute an?"
- „Daily Briefing."

## Installation

1. `SKILL.md` aus diesem Ordner herunterladen.
2. In Claude (Cowork, Claude Code oder Claude Desktop) als eigenen Skill hinzufügen.
3. Los — beim allerersten Start fragt der Skill kurz nach Ort, gewünschten Integrationen (Kalender/Mail/Aufgaben) und bevorzugten Abschnitten, danach merkt er sich das für alle weiteren Male.

## Anwendungsbeispiele

**Beispiel 1**
Du: „Mach mir ein Morgen-Dashboard."
Ergebnis: Claude liest verfügbare Kalender-, Mail- und Aufgabendaten aus, priorisiert die drei wichtigsten Punkte des Tages und legt eine HTML-Datei `morgen-dashboard-JJJJ-MM-TT-HHmm.html` an, die automatisch im Browser geöffnet wird.

**Beispiel 2**
Du: „Hier sind meine Termine, Mails und Aufgaben. Bau mir daraus ein Tages-Dashboard." (ohne verbundene Integrationen)
Ergebnis: Claude verwendet die im Chat mitgegebenen Daten und erstellt daraus dasselbe Dashboard-Format.

## Voraussetzungen

Keine bestimmte Integration ist Pflicht — der Skill funktioniert mit jeder verbundenen Integration (Google, Microsoft, Apple, Notion, Asana u. a.) oder mit Daten, die du direkt im Chat mitgibst. Für die volle Breite im Browser hilft die Claude-in-Chrome-Erweiterung; ohne sie öffnest du das Dashboard über das Vorschau-Menü.

## Was ist neu in dieser Version

**v1.0.0** — Erste Veröffentlichung (Juni 2026): Tages-Dashboard als einzelne HTML-Datei (Kalender, Aufgaben, Inbox, Wetter, News), Einstellungs-Gedächtnis mit Onboarding beim ersten Start, automatisches Öffnen im Browser, Hell/Dunkel-Toggle, Abhak-Checkboxen, automatisches Aufräumen alter Dashboards nach 7 Tagen.

## Wenn etwas nicht klappt

- Es öffnet sich kein Dashboard im Browser? → Ohne Claude-in-Chrome-Erweiterung öffnest du die Datei manuell über das Vorschau-Menü ("In Google Chrome öffnen").
- Falsche oder fehlende Daten? → Der Skill erfindet nie Termine, Mails oder Aufgaben; fehlende Daten werden als „nicht verfügbar" markiert.
- Einstellungen ändern? → Einfach sagen, z. B. „ändere meinen Ort auf Berlin" — der Skill aktualisiert seine gespeicherten Einstellungen direkt.

## Herkunft & Lizenz

Eigenentwicklung von KI-Wissen.org (Harald Frey). Dieses Projekt steht unter der **Apache License 2.0** (siehe `LICENSE`).

---
Fragen oder Probleme? → https://ki-wissen.org · Ein Skill von KI-Wissen.org (Harald Frey)
