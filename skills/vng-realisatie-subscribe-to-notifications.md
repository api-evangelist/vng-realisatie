---
generated: '2026-10-09'
method: generated
name: subscribe-to-notifications
description: Subscribe a webhook callback to events in the Notificaties API.
api: openapi/vng-realisatie-notificaties-openapi.yml
operations:
- domain_list
- subscription_create
- subscription_read
source: Grounded in openapi/vng-realisatie-notificaties-openapi.yml; every operationId verified verbatim in the spec.
---

# Subscribe a webhook callback to events in the Notificaties API.

## Steps

1. `domain_list` (GET /domains) to find the domain whose events you need.
2. `subscription_create` (POST /subscriptions) with your callback endpoint and filters.
3. `subscription_read` (GET /subscriptions/{uuid}) to verify it.

## Rules

- Auth: send `Authorization: Bearer <JWT>` (the contract's `JWT-Claims` HTTP bearer scheme); a missing/invalid token returns 401, insufficient scopes 403.
- This contract is version 2.0.0-alpha13; expect changes.
- The contract declares no idempotency key: before retrying a failed POST, search/list first to avoid creating a duplicate.
