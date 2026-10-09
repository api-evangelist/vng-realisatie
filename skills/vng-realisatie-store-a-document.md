---
generated: '2026-10-09'
method: generated
name: store-a-document
description: Create an informatieobject in the Documenten API, upload its content in parts under a lock, then download it.
api: openapi/vng-realisatie-documenten-openapi.yml
operations:
- enkelvoudiginformatieobject_create
- enkelvoudiginformatieobject_lock
- bestandsdeel_update
- enkelvoudiginformatieobject_unlock
- enkelvoudiginformatieobject_download
- enkelvoudiginformatieobject_partial_update
source: Grounded in openapi/vng-realisatie-documenten-openapi.yml; every operationId verified verbatim in the spec.
---

# Create an informatieobject in the Documenten API, upload its content in parts under a lock, then download it.

## Steps

1. `enkelvoudiginformatieobject_create` (POST /enkelvoudiginformatieobjecten) with metadata and `informatieobjecttype` URL.
2. `enkelvoudiginformatieobject_lock` (POST .../{uuid}/lock) to obtain a lock before changing content.
3. `bestandsdeel_update` (PUT /bestandsdelen/{uuid}) for each file part returned on the object.
4. `enkelvoudiginformatieobject_unlock` (POST .../{uuid}/unlock, 204) to release; use `enkelvoudiginformatieobject_partial_update` for metadata changes while locked.
5. `enkelvoudiginformatieobject_download` (GET .../{uuid}/download) to fetch the binary.

## Rules

- Auth: send `Authorization: Bearer <JWT>` (the contract's `JWT-Claims` HTTP bearer scheme); a missing/invalid token returns 401, insufficient scopes 403.
- Write operations accept the optional `X-NLX-Logrecord-ID` and `X-Audit-Toelichting` headers (audit trail).
- The contract declares no idempotency key: before retrying a failed POST, search/list first to avoid creating a duplicate.
- Always unlock after a failed upload so the object is not left locked.
