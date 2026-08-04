# CloudBees (cloudbees)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

CloudBees provides software delivery automation across continuous integration, continuous deployment, release orchestration, and feature management. Their developer surface includes the CloudBees CI REST API (an extension of the Jenkins REST API), the CloudBees CD/RO REST API for release orchestration, the CloudBees Feature Management REST API (formerly Rollout) for feature flags and environments, and the CloudBees Unify Platform API for the modern unified delivery platform. APIs are generally JSON, token-authenticated, and follow REST conventions.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cloudbees/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cloudbees/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- CI/CD
- Continuous Delivery
- Continuous Integration
- DevOps
- Feature Flags
- Feature Management
- Jenkins
- Release Orchestration
- Software Delivery

## Timestamps

- **Created:** 2025-01-08
- **Modified:** 2026-04-23

## APIs

### CloudBees CI REST API

CloudBees CI is a hardened, enterprise distribution of Jenkins. The REST API is the Jenkins remote access API exposed at /api on every controller and on individual jobs, runs, queues and nodes. Callers authenticate with a username and API token in HTTP basic auth and can list/create jobs, trigger builds, fetch build status and console logs, manage credentials, and inspect operations centers. Responses are available as JSON, XML, or Python.

- **Human URL:** [https://docs.cloudbees.com/docs/cloudbees-ci-kb/latest/best-practices/best-practice-for-using-jenkins-rest-api](https://docs.cloudbees.com/docs/cloudbees-ci-kb/latest/best-practices/best-practice-for-using-jenkins-rest-api)
- **Base URL:** `https://example.cloudbees.com`

#### Tags

- CI/CD
- Continuous Integration
- Jenkins
- Pipelines

#### Properties

- [Documentation](https://docs.cloudbees.com/docs/cloudbees-ci-kb/latest/best-practices/best-practice-for-using-jenkins-rest-api)
- [Release Notes](https://docs.cloudbees.com/docs/release-notes/latest/cloudbees-ci/)
- [Postman Collection](collections/cloudbees.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudbees.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudBees CD/RO REST API

The CloudBees CD/RO (Continuous Delivery / Release Orchestration) REST API exposes resources for pipelines, releases, environments, applications, deployments, projects and resources. Operations cover modelling deployment pipelines, launching releases, tracking stages, managing environments and inventories, and integrating with Jenkins and other CI tools.

- **Human URL:** [https://docs.cloudbees.com/docs/cloudbees-cd/latest/api/](https://docs.cloudbees.com/docs/cloudbees-cd/latest/api/)
- **Base URL:** `https://example-cd.cloudbees.com/rest/v1.0`

#### Tags

- Continuous Delivery
- DevOps
- Pipelines
- Release Orchestration

#### Properties

- [Documentation](https://docs.cloudbees.com/docs/cloudbees-cd/latest/api/)
- [Jenkins  Plugin](https://docs.cloudbees.com/plugins/cd/ec-jenkins)
- [Postman Collection](collections/cloudbees.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudbees.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudBees Feature Management REST API

The CloudBees Feature Management REST API (formerly Rollout) provides programmatic access to applications, environments, feature flags, experiments, target groups, audit logs, and users. Authentication uses a bearer token in the Authorization header. The API enforces a one request per second rate limit per IP, returning HTTP 555 when exceeded.

- **Human URL:** [https://docs.cloudbees.com/docs/cloudbees-feature-management-rest-api/latest/introduction](https://docs.cloudbees.com/docs/cloudbees-feature-management-rest-api/latest/introduction)
- **Base URL:** `https://x-api.rollout.io/public-api`

#### Tags

- Experimentation
- Feature Flags
- Feature Management

#### Properties

- [Documentation](https://docs.cloudbees.com/docs/cloudbees-feature-management-rest-api/latest/introduction)
- [Environments](https://docs.cloudbees.com/docs/cloudbees-feature-management-rest-api/latest/environments)
- [Reference](https://docs.cloudbees.com/docs/cloudbees-feature-management/latest/rest-api)
- [Postman Collection](collections/cloudbees.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudbees.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudBees Unify Platform API

CloudBees Unify is the modern, opinionated software delivery platform that unifies CI, CD, feature management, analytics, and security into a single workflow. The platform exposes APIs for managing organizations, components, workflows, environments, feature flags, and analytics; authentication is via personal access tokens and the surface is the recommended target for new integrations.

- **Human URL:** [https://docs.cloudbees.com/](https://docs.cloudbees.com/)

#### Tags

- DevOps
- Platform
- Software Delivery

#### Properties

- [Documentation](https://docs.cloudbees.com/)
- [Postman Collection](collections/cloudbees.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudbees.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CloudBees CD/RO Jenkins Plugin Steps

The CloudBees CD plugin for Jenkins exposes Jenkins pipeline steps that call CloudBees CD/RO REST endpoints — triggering pipelines, running releases, deploying applications, and pulling artifacts from Jenkins build outputs into CD/RO release flows.

- **Human URL:** [https://www.jenkins.io/doc/pipeline/steps/electricflow/](https://www.jenkins.io/doc/pipeline/steps/electricflow/)

#### Tags

- Continuous Delivery
- Jenkins
- Plugin

#### Properties

- [Documentation](https://www.jenkins.io/doc/pipeline/steps/electricflow/)
- [Plugin](https://plugins.jenkins.io/electricflow)
- [Postman Collection](collections/cloudbees.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudbees.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/cloudbees)
- [LinkedIn](https://www.linkedin.com/company/cloudbees)
- [Website](https://www.cloudbees.com/)
- [Documentation](https://docs.cloudbees.com/)
- [Support](https://support.cloudbees.com/)
- [Privacy Policy](https://www.cloudbees.com/privacy)
- [Plugins](https://docs.cloudbees.com/plugins/ci)
- [JSON-LD](json-ld/cloudbees-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Spectral Rules](rules/cloudbees-rules.yml) — [Spectral](https://docs.stoplight.io/docs/spectral)
- [Integrations](https://www.cloudbees.com/partners)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
