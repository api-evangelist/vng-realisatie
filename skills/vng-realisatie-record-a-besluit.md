---
generated: '2026-10-09'
method: generated
name: record-a-besluit
description: Record a decision (BESLUIT) in the Besluiten API and attach its supporting document.
api: openapi/vng-realisatie-besluiten-openapi.yml
operations:
- besluit_create
- besluitinformatieobject_create
- besluit_read
source: Grounded in openapi/vng-realisatie-besluiten-openapi.yml; every operationId verified verbatim in the spec.
---

# Record a decision (BESLUIT) in the Besluiten API and attach its supporting document.

## Steps

1. `besluit_create` (POST /besluiten) with the `besluittype` URL (and optionally the zaak URL).
2. `besluitinformatieobject_create` (POST /besluitinformatieobjecten) linking a Documenten API informatieobject.
3. `besluit_read` (GET /besluiten/{uuid}) to confirm.

## Rules

- Auth: send `Authorization: Bearer <JWT>` (the contract's `JWT-Claims` HTTP bearer scheme); a missing/invalid token returns 401, insufficient scopes 403.
- Write operations accept the optional `X-NLX-Logrecord-ID` and `X-Audit-Toelichting` headers (audit trail).
- The contract declares no idempotency key: before retrying a failed POST, search/list first to avoid creating a duplicate.
