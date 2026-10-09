---
generated: '2026-10-09'
method: generated
name: publish-a-zaaktype
description: Configure a case type (ZAAKTYPE) with its status, role and result types in the Catalogi API and publish it.
api: openapi/vng-realisatie-catalogi-openapi.yml
operations:
- catalogus_list
- zaaktype_create
- statustype_create
- roltype_create
- resultaattype_create
- zaaktype_publish
source: Grounded in openapi/vng-realisatie-catalogi-openapi.yml; every operationId verified verbatim in the spec.
---

# Configure a case type (ZAAKTYPE) with its status, role and result types in the Catalogi API and publish it.

## Steps

1. `catalogus_list` (GET /catalogussen) to pick the catalogus URL.
2. `zaaktype_create` (POST /zaaktypen) as a concept.
3. `statustype_create`, `roltype_create`, `resultaattype_create` referencing the concept zaaktype.
4. `zaaktype_publish` (POST /zaaktypen/{uuid}/publish) to make it usable by the Zaken API.

## Rules

- Auth: send `Authorization: Bearer <JWT>` (the contract's `JWT-Claims` HTTP bearer scheme); a missing/invalid token returns 401, insufficient scopes 403.
- The contract declares no idempotency key: before retrying a failed POST, search/list first to avoid creating a duplicate.
