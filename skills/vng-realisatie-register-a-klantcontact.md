---
generated: '2026-10-09'
method: generated
name: register-a-klantcontact
description: Register a customer contact in Klantinteracties and route follow-up as an internal task.
api: openapi/vng-realisatie-klantinteracties-openapi.yml
operations:
- registreerklantcontact
- registreerinternetaak
- zoekinternetaak
- markeerinternetaakverwerkt
source: Grounded in openapi/vng-realisatie-klantinteracties-openapi.yml; every operationId verified verbatim in the spec.
---

# Register a customer contact in Klantinteracties and route follow-up as an internal task.

## Steps

1. `registreerklantcontact` (POST /_registreer_klantcontact).
2. `registreerinternetaak` (POST /_registreer_interne_taak) for follow-up.
3. `zoekinternetaak` (POST /_zoek_interne_taak) to find open tasks.
4. `markeerinternetaakverwerkt` (POST /_markeer_interne_taak_verwerkt) when done.

## Rules

- This contract (version 00.01.00, servers on SwaggerHub mock / voorbeeldgemeente.nl) declares no security scheme; authentication is set by the implementing municipality.
- The contract declares no idempotency key: before retrying a failed POST, search/list first to avoid creating a duplicate.
