# Veröffentlichung auf Cloudflare R2

Exklusive Skills werden im R2-Bucket `ki-wissen-downloads` veröffentlicht;
Harald gibt den Download-Link an seine User weiter.

## Voraussetzungen

- Zugangsdaten + Upload-Skript liegen in `Speicher/Skill-Center/`:
  `cloudflare-r2.md` (Endpoint, Keys, Domain — VERTRAULICH) und `r2-upload.py`.
- Fehlen sie → Harald bitten, den Ordner zuzuordnen oder die Dateien wiederherzustellen.
- Der Skill muss Status **freigegeben ✅** haben und Befehl 6 (inkl. Security- und
  Standard-Check) durchlaufen haben. **Niemals die Zugangsdaten-Datei mit ins
  Skill-Paket packen** — das prüft der Security-Check ausdrücklich.

## Upload (automatisch)

```bash
cd Speicher/Skill-Center
python3 r2-upload.py <pfad-zur-datei>.skill <skill-name> <version>
```

Das Skript erledigt die bekannten Problemquellen automatisch:

| Problem früher | Lösung im Skript |
|---|---|
| Datei beschädigt hochgeladen | ZIP-Magic-Check vor Upload, Größen-Verifikation danach |
| Browser benennt um / zeigt Inhalt an | `Content-Type: application/zip` + `Content-Disposition: attachment` mit korrektem Dateinamen |
| User bekommen alte Version | Stabiler Pfad mit `Cache-Control: no-cache` — Link bleibt gleich, Inhalt immer aktuell |
| Versionschaos | Zusätzlich versioniertes Archiv unter `skills/archiv/…` (unveränderlich, langer Cache) |

## Pfad-Schema

- `skills/<skill-name>.skill` — **dieser Link geht an die User** (immer aktuellste Version)
- `skills/archiv/<skill-name>-v<x.y.z>.skill` — Archiv, falls eine bestimmte Version gebraucht wird

Download-URL = öffentliche Bucket-Domain + Pfad. Die Domain steht in `cloudflare-r2.md`.

## Nach dem Upload

1. **Download-Link verifizieren:** URL per `web_fetch`/curl-Äquivalent prüfen — kommt
   HTTP 200 mit `application/zip`? Wenn 401/404: Public Access des Buckets ist nicht
   aktiv → Harald an Dashboard → Bucket → Settings → Public access erinnern.
2. Im REGISTER vermerken: „veröffentlicht am <Datum>, v<version>, Link: <URL>".
3. Harald den fertigen User-Link nennen.

## Hinweisblock für User (in README jedes veröffentlichten Skills aufnehmen)

```
## Download & Installation
1. Lade die Datei über den Link herunter: <URL>
2. Safari-Nutzer: Falls die Datei automatisch entpackt wurde (Ordner statt .skill-Datei),
   in Safari → Einstellungen → Allgemein das automatische Öffnen „sicherer" Dateien
   deaktivieren und erneut herunterladen.
3. Ziehe die .skill-Datei mit der Maus direkt in das Chatfeld von Claude Cowork
   (über das Plus-Zeichen funktioniert es nicht).
4. Schreibe „Installiere den Skill" und speichere ihn am Ende über den Button —
   falls kein Button erscheint, schreibe „bitte abspeichern".
5. Starte eine neue Unterhaltung — fertig.
```
