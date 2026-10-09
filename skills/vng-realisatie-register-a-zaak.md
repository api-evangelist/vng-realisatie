---
generated: '2026-10-09'
method: generated
name: register-a-zaak
description: Register a case (ZAAK) in the Zaken API, set its status, link involved parties and documents, then read it back.
api: openapi/vng-realisatie-zaken-openapi.yml
operations:
- zaak_create
- status_create
- rol_create
- zaakinformatieobject_create
- zaak_retrieve
- zaak__zoek
source: Grounded in openapi/vng-realisatie-zaken-openapi.yml; every operationId verified verbatim in the spec.
---

# Register a case (ZAAK) in the Zaken API, set its status, link involved parties and documents, then read it back.

## Steps

1. `zaak_create` (POST /zaken) with the `zaaktype` URL from the Catalogi API; keep the returned `url`.
2. `status_create` (POST /statussen) referencing the zaak URL and a `statustype` from the zaaktype.
3. `rol_create` (POST /rollen) to attach an initiator or handler with a `roltype` of the zaaktype.
4. `zaakinformatieobject_create` (POST /zaakinformatieobjecten) to link a document stored via the Documenten API.
5. `zaak_retrieve` (GET /zaken/{uuid}) to confirm; use `zaak__zoek` (POST /zaken/_zoek) for (geo)search.

## Rules

- Auth: send `Authorization: Bearer <JWT>` (the contract's `JWT-Claims` HTTP bearer scheme); a missing/invalid token returns 401, insufficient scopes 403.
- Write operations accept the optional `X-NLX-Logrecord-ID` and `X-Audit-Toelichting` headers (audit trail).
- `zaak_create` and `zaak_retrieve` take `Accept-Crs`/`Content-Crs` headers for geometry.
- The contract declares no idempotency key: before retrying a failed POST, search/list first to avoid creating a duplicate.
- 400 responses carry field-level validation errors; fix the body rather than retrying.
