# DNS-Provider-API — exakte, LIVE GETESTETE Aufrufe (10.06.2026)
# IONOS: Anlegen UND Löschen verifiziert.

═══════════════════════════════════════════════════════════════════
IONOS (Developer/Hosting-API) — REST, ein Header
═══════════════════════════════════════════════════════════════════
- Key holen: developer.hosting.ionos.DE (Inkognito + Hauptkonto). Format PREFIX.SECRET.
- API-HOST: https://api.hosting.ionos.COM/dns/v1   (.de antwortet NICHT)
- Header:   X-API-Key: PREFIX.SECRET
- Frisch erstellter Key kann ~Sekunden brauchen (erst 401, dann 200) → kurz retry.

Zonen listen (findet zoneId der Domain):
  curl -s -H "X-API-Key: $KEY" https://api.hosting.ionos.com/dns/v1/zones
  → [{"name":"example.com","id":"<zoneId>","type":"NATIVE"}, ...]

Records einer Zone lesen:
  curl -s -H "X-API-Key: $KEY" https://api.hosting.ionos.com/dns/v1/zones/<zoneId>
  → {"records":[{"name":"<FQDN>","type":"A","content":"<ip>","id":"<recId>",...}]}

A-Record anlegen (name = VOLLER FQDN!):
  curl -s -X POST https://api.hosting.ionos.com/dns/v1/zones/<zoneId>/records \
    -H "X-API-Key: $KEY" -H "Content-Type: application/json" \
    -d '[{"name":"coolify.example.com","type":"A","content":"<IP>","ttl":300,"disabled":false}]'
  → HTTP 201, Antwort enthält "id" des Records.

A-Record löschen:
  curl -s -X DELETE https://api.hosting.ionos.com/dns/v1/zones/<zoneId>/records/<recId> \
    -H "X-API-Key: $KEY"   → HTTP 200

Idempotenz: vor dem Anlegen Records lesen; existiert "coolify.example.com" schon →
  alten Record per DELETE entfernen und neu anlegen (oder unverändert lassen, wenn IP stimmt).

Domain-Auflistung: IONOS KANN Zonen listen (GET /zones) — Domain automatisch findbar.
Bei mehreren Zonen den Nutzer die richtige bestätigen lassen.

═══════════════════════════════════════════════════════════════════
Propagation prüfen, bevor SSL ausgelöst wird
═══════════════════════════════════════════════════════════════════
  dig +short A <sub>.<domain> @1.1.1.1
  dig +short A <sub>.<domain> @8.8.8.8
  dig +short A <sub>.<domain> @<autoritativer NS>
Alle müssen die server_ip liefern. Erst dann Coolify-fqdn setzen (sonst LE-Fehler).
IONOS: meist <1 Min (frische Subdomain).
