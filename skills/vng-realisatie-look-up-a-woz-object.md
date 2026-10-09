---
generated: '2026-10-09'
method: generated
name: look-up-a-woz-object
description: Look up WOZ (property valuation) objects via WOZ bevragen.
api: openapi/vng-realisatie-woz-bevragen-openapi.yml
operations:
- getwozobjecten
- getwozobject
source: Grounded in openapi/vng-realisatie-woz-bevragen-openapi.yml; every operationId verified verbatim in the spec.
---

# Look up WOZ (property valuation) objects via WOZ bevragen.

## Steps

1. `getwozobjecten` (GET /wozobjecten) with search filters.
2. `getwozobject` (GET /wozobjecten/{wozobjectnummer}) for one object.

## Rules

- Read-only. The contract (0.9.0) declares no security scheme and uses an `acceptCrs` parameter for geometry.
