---
name: Record a CloudBees Unify delivery run
description: >-
  Create a run against a component in the CloudBees Unify v4 API and attach the evidence a governed
  delivery record needs — test results, artifacts, security results, deployments — then close the run out.
api: openapi/cloudbees-unify-beta-openapi.yml
operations:
  - listComponents
  - getComponent
  - createRun
  - createTestResults
  - createArtifacts
  - createSecurityResults
  - createEvidences
  - createDeploymentArtifacts
  - updateRun
  - getRun
generated: '2026-09-05'
method: generated
source: openapi/cloudbees-unify-beta-openapi.yml + conventions/cloudbees-conventions.yml
---

# Record a CloudBees Unify delivery run

Base URL `https://api.cloudbees.io`. `Authorization: Bearer <personal_access_token>`.

This is the v4 (beta) surface. CloudBees describes it as production-ready but evolving, and directs new
integrations here rather than to the v1/v2/v3 endpoints.

## The shape of the thing

A **run** is the join point of the delivery record. A component is a source repository; a run belongs to a
component; and every piece of evidence a governance review will later ask for hangs off that one run id.
Get the run id right and everything else attaches; get it wrong and the evidence lands on someone else's
delivery.

## Steps

1. `listComponents` — `GET /v4/organizations/{orgId}/components`. Find the component for the repository.
   Filter with `repositoryUrl` or `name` rather than paging the whole list.
2. `getComponent` — `GET /v4/organizations/{orgId}/components/{id}` if you need to confirm the component
   before writing to it.
3. `createRun` — `POST /v4/components/{componentId}/runs`. **Keep the returned run id.** This POST is not
   idempotent: calling it twice creates two runs, and there is no operation to delete one.
4. Attach evidence, in any order, all scoped to `/v4/components/{componentId}/runs/{runId}/…`:
   - `createTestResults` — `POST …/test-results`
   - `createArtifacts` — `POST …/artifacts`
   - `createSecurityResults` — `POST …/security-results`
   - `createEvidences` — `POST …/evidences`
   - `createDeploymentArtifacts` — `POST …/deployments`
5. `updateRun` — `PATCH /v4/components/{componentId}/runs/{run.id}`. Set the terminal status.
6. `getRun` — `GET /v4/components/{componentId}/runs/{runId}` to verify. The matching `list…` operation
   exists for each evidence type if you need to read back what attached.

## Rules that apply to every step

- **Evidence ingestion is append-only.** There is no delete and no amend on artifacts, evidences, test
  results, security results or deployments. A wrong submission cannot be withdrawn through the API. Validate
  before you POST — this is the least reversible surface CloudBees publishes.
- **No idempotency key.** On a timeout after `createRun`, do not retry: read back before writing again.
- **Cursor pagination on v4:** `pageSize`, `pageToken`, `orderBy`; follow `nextPageToken`. This is the
  Google AIP-158 shape and it is *not* what the v1/v2 endpoints use.
- **Errors:** only `200` and a `default` `google.rpc.Status` are declared. No 4xx is enumerated, so treat
  any non-200 as terminal unless you have independent reason to retry.
- **No published rate limit** on `api.cloudbees.io` — which means no headers to pace against either. Batch
  evidence rather than firing one request per test case.
