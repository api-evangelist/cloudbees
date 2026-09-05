---
name: Roll out a CloudBees feature flag safely
description: >-
  Find a CloudBees Feature Management flag by name, read its configuration in the target environment,
  enable it, and confirm what is actually being served — with the rollback path established before the
  change is made.
api: openapi/cloudbees-unify-openapi.yml
operations:
  - listOrganizations
  - ReportServiceHandler_GetEnvironmentsv2
  - FlagApi_GetFlagByName
  - FlagConfigurationApi_GetFlagConfiguration
  - FlagConfigurationApi_UpdateFlagConfigurationConfigState
  - FlagApi_GetFlagFlagUsagePerEnvironment
generated: '2026-09-05'
method: generated
source: openapi/cloudbees-unify-openapi.yml + conventions/cloudbees-conventions.yml
---

# Roll out a CloudBees feature flag safely

Base URL `https://api.cloudbees.io`. Every request carries
`Authorization: Bearer <personal_access_token>`. The token inherits the permissions of the user who
created it, so check that the user can write flag configurations in the target environment before starting.

## Before you change anything

A flag's behaviour is never global. It is always the triple **(application, flag, environment)**. You need
three ids, and a change to the wrong environment is indistinguishable from a change to the right one until
someone notices.

1. `listOrganizations` — `GET /v1/organizations`. Confirm which organization you are operating in.
2. `ReportServiceHandler_GetEnvironmentsv2` — `GET /v2/organizations/{orgId}/environments`. Get the
   `environmentId` for the environment you intend to change. Do not guess it from a name you remember.
3. `FlagApi_GetFlagByName` — `GET /v2/applications/{applicationId}/flags/by-name/{name}`. Resolve the flag
   name to its `flagId`.

## Read the current state — this is your rollback

4. `FlagConfigurationApi_GetFlagConfiguration` —
   `GET /v2/applications/{applicationId}/flags/{flagId}/configuration/environments/{environmentId}`.

**Keep this response.** CloudBees publishes no revert operation and no prior-value snapshot. If you overwrite
a configuration and did not retain the previous one, you cannot restore it through the API — per-flag audit
logs will show you what changed, but there is no operation to put it back. This response is the only
rollback you will have.

## Make the change

5. `FlagConfigurationApi_UpdateFlagConfigurationConfigState` —
   `POST /v2/applications/{applicationId}/flags/{flagId}/configuration/environments/{environmentId}/configstate`.

This toggles the configuration state. It is symmetric: the same operation turns it back off, so enabling is
reversible immediately and no window applies.

If you need to change targeting rather than just on/off, use
`FlagConfigurationApi_PatchFlagConfiguration` (PATCH, partial) or
`FlagConfigurationApi_UpdateFlagConfiguration` (PUT, whole body) on the same path. Prefer PATCH — the PUT
replaces the configuration and will silently drop conditions you did not resend.

## Confirm what is actually served

6. `FlagApi_GetFlagFlagUsagePerEnvironment` —
   `GET /v2/applications/{applicationId}/flags/{id}/flag-usage-per-environment`. Impression data tells you
   which variation real evaluations received. A 200 on the update means the configuration was written; only
   this tells you the rollout is doing what you meant.

## Rules that apply to every step

- **No idempotency.** There is no `Idempotency-Key` on any CloudBees operation. Never blind-retry a POST.
  On a timeout, re-read with `FlagConfigurationApi_GetFlagConfiguration` and decide from the current state.
- **Errors are thin.** Every operation declares only `200` and a `default` error bound to
  `google.rpc.Status`. The contract does not tell you which 4xx are reachable. A live unauthenticated call
  returns `{"error": "..."}`, which does not match the declared shape — parse defensively.
- **Pagination on this generation is page-number:** `pagination.page`, `pagination.pageLength`,
  `pagination.sort.fieldName`, `pagination.sort.order`. (The v4 beta API uses `pageSize`/`pageToken`
  instead — do not mix them.)
- **Rate limits are undocumented on `api.cloudbees.io`.** No published limit and no rate-limit headers.
  The separate Feature Management REST API on `x-api.rollout.io` is limited to 1 request/second per IP and
  answers `HTTP 555` when exceeded — a non-standard status your client must special-case.
