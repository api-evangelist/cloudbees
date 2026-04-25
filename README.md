# CloudBees (cloudbees)

CloudBees provides software delivery automation across continuous integration, continuous deployment, release orchestration, and feature management. Their developer surface includes the CloudBees CI REST API (an extension of the Jenkins REST API), the CloudBees CD/RO REST API for release orchestration, the CloudBees Feature Management REST API (formerly Rollout) for feature flags and environments, and the CloudBees Unify Platform API for the modern unified delivery platform. APIs are generally JSON, token-authenticated, and follow REST conventions.

**APIs.json:** [apis.yml](https://raw.githubusercontent.com/api-evangelist/cloudbees/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party
- **x-type:** company

## Tags

CI/CD, Continuous Delivery, Continuous Integration, DevOps, Feature Flags, Feature Management, Jenkins, Release Orchestration, Software Delivery

## Timestamps

- **Created:** 2025-01-08
- **Modified:** 2026-04-23

## APIs

### CloudBees CI REST API
CloudBees CI is a hardened, enterprise distribution of Jenkins. The Jenkins remote access API is exposed at `/api` on every controller and on individual jobs, runs, queues and nodes. Authentication uses a username plus API token via HTTP basic auth. Responses are available as JSON, XML, or Python.

- [Best Practice for Jenkins REST API](https://docs.cloudbees.com/docs/cloudbees-ci-kb/latest/best-practices/best-practice-for-using-jenkins-rest-api)
- [Release Notes](https://docs.cloudbees.com/docs/release-notes/latest/cloudbees-ci/)

### CloudBees CD/RO REST API
The Continuous Delivery / Release Orchestration REST API exposes pipelines, releases, environments, applications, deployments, projects and resources. Use it to model deployment pipelines, launch releases, track stages, and integrate with Jenkins and other CI tools.

- Base URL: `https://<your-server>/rest/v1.0`
- [Documentation](https://docs.cloudbees.com/docs/cloudbees-cd/latest/api/)
- [Jenkins Plugin](https://docs.cloudbees.com/plugins/cd/ec-jenkins)

### CloudBees Feature Management REST API
Programmatic access to applications, environments, feature flags, experiments, target groups, audit logs, and users. Authentication is a bearer token. The API enforces one request per second per IP, returning HTTP 555 when exceeded.

- Base URL: `https://x-api.rollout.io/public-api`
- [Documentation](https://docs.cloudbees.com/docs/cloudbees-feature-management-rest-api/latest/introduction)
- [Environments](https://docs.cloudbees.com/docs/cloudbees-feature-management-rest-api/latest/environments)
- [Reference](https://docs.cloudbees.com/docs/cloudbees-feature-management/latest/rest-api)

### CloudBees Unify Platform API
The modern, opinionated software delivery platform that unifies CI, CD, feature management, analytics, and security. Recommended target for new integrations.

- [Documentation](https://docs.cloudbees.com/)

### CloudBees CD/RO Jenkins Plugin Steps
Jenkins pipeline steps that call CloudBees CD/RO REST endpoints — triggering pipelines, running releases, deploying applications, and pulling artifacts from Jenkins build outputs into CD/RO release flows.

- [Documentation](https://www.jenkins.io/doc/pipeline/steps/electricflow/)
- [Plugin](https://plugins.jenkins.io/electricflow)

## Common Properties

- [Website](https://www.cloudbees.com/)
- [Documentation](https://docs.cloudbees.com/)
- [Support](https://support.cloudbees.com/)
- [Privacy Policy](https://www.cloudbees.com/privacy)
- [Plugins](https://docs.cloudbees.com/plugins/ci)
- [JSON-LD](json-ld/cloudbees-context.jsonld)
- [Spectral](rules/cloudbees-rules.yml)
- [Naftiko Capabilities](capabilities/feature-management.yaml)

## Maintainers

- **FN:** Kin Lane
- **Email:** kin@apievangelist.com
