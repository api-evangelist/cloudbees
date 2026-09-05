---
name: Audit CloudBees Unify org and team access
description: >-
  Enumerate organizations, teams, memberships and users in CloudBees Unify to answer "who can reach what",
  using only read operations, then make a scoped membership change.
api: openapi/cloudbees-unify-beta-openapi.yml
operations:
  - listOrganizations
  - getOrganizationByName
  - TeamsService_GetTeams
  - listTeams
  - getTeam
  - listTeamMemberships
  - getTeamMembership
  - listUsers
  - createTeamMembership
  - deleteTeamMembership
generated: '2026-09-05'
method: generated
source: >-
  openapi/cloudbees-unify-openapi.yml + openapi/cloudbees-unify-beta-openapi.yml +
  conventions/cloudbees-conventions.yml
---

# Audit CloudBees Unify org and team access

Base URL `https://api.cloudbees.io`. `Authorization: Bearer <personal_access_token>`.

The token inherits its creator's permissions, so an audit run with a low-privilege token returns a
truthful-looking but incomplete picture. Confirm the token's reach before trusting an empty result.

## Read pass — nothing here changes state

1. `listOrganizations` — `GET /v1/organizations`. Use the `nested` query parameter to see the hierarchy;
   organizations nest parent-to-child and inherit properties, integrations and environments downward.
   `getOrganizationByName` — `GET /v1/organizations/name` — resolves a known name.
2. Teams, in either generation:
   - `listTeams` — `GET /v4/teams` (tenant-scoped, v4, cursor pagination)
   - `TeamsService_GetTeams` — `GET /v1/organizations/{organizationId}/teams` (org-scoped, v1)
   `getTeam` — `GET /v4/teams/{id}` — accepts `include` to expand users in one call rather than fanning out.
3. `listTeamMemberships` — `GET /v4/teams/{teamId}/memberships`. `getTeamMembership` —
   `GET /v4/teams/{teamId}/memberships/{userId}` — checks one person.
4. `listUsers` — `GET /v4/users`. Filter with `email` or `name`.

## What the REST API will not tell you

Roles and permissions are **not** in the public REST contract. `rbac_roles_list`,
`rbac_permissions_list`, `rbac_authorizations_list` and `rbac_authorization_check_bulk` exist only as
CloudBees Unify MCP tools (`https://mcp.cloudbees.io/v1/mcp`). A REST-only audit can establish *who is in
which team*; it cannot establish *what that team is allowed to do*. Say so in the finding rather than
implying the audit was complete. The same applies to SAML connections and API token inventory.

## Write pass — only when the audit calls for a change

- `createTeamMembership` — `POST /v4/teams/{teamId}/memberships`
- `deleteTeamMembership` — `DELETE /v4/teams/{teamId}/memberships/{userId}`

These are inverses of each other, so a membership change is reversible by re-adding — but re-adding is a
new membership, not a restore, and no window is published for anything here. Removing a user from the
organization entirely (`MembershipsService_RemoveUsersFromTeamV3`, `DELETE
/v3/organizations/{organizationId}/user/{userId}`) is reversed only by issuing a fresh invitation
(`InvitesService_CreateInviteV3`) that the person must accept. Treat org removal as one-way.

## Rules that apply to every step

- **No idempotency key.** `createTeamMembership` retried after a timeout may not be safe; read back with
  `getTeamMembership` first.
- **Two pagination styles.** v1/v2 use `pagination.page`/`pagination.pageLength`; v4 uses
  `pageSize`/`pageToken`. Mixing them silently returns page one forever.
- **Errors:** `200` plus a `default` `google.rpc.Status`; no enumerated 4xx.
