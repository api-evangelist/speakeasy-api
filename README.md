# Speakeasy (speakeasy-api)

Speakeasy is an API developer-experience platform that generates production-ready, type-safe SDKs (client libraries), Terraform providers, MCP servers, CLIs, contract tests, code samples, and docs directly from an OpenAPI specification. It is OpenAPI-native, with no proprietary DSL and no lock-in.

## How you actually use Speakeasy (access model)

Speakeasy is a **developer-tool platform**, not a hosted runtime data API. There are three ways in, and it is worth being clear about which is which:

1. **Speakeasy CLI** (primary interface) - open source at [github.com/speakeasy-api/speakeasy](https://github.com/speakeasy-api/speakeasy), installed via Homebrew, install script, Winget, or Chocolatey. This is how most teams generate and manage SDKs day to day.
2. **Speakeasy GitHub Action** - [github.com/speakeasy-api/sdk-generation-action](https://github.com/speakeasy-api/sdk-generation-action) - runs generation, release, and publishing in CI so SDKs stay in lock-step with the API.
3. **Hosted platform + public REST API** - the web dashboard and a **documented public REST API** at `https://api.prod.speakeasy.com`, which the CLI and Action call underneath. Its OpenAPI 3.0.3 document is published at [speakeasy.com/openapi.yaml](https://www.speakeasy.com/openapi.yaml) (title "Speakeasy API", version 0.4.0).

So the REST API is real and documented, but it is a **platform / registry control plane** - workspaces, organizations, an OpenAPI/artifact registry, schema store, code samples, generation events, lint and change reports, GitHub automation, LLM OpenAPI suggestions, publishing tokens, and event subscriptions - rather than a general-purpose data API you would build an app against. The `openapi/speakeasy-api-openapi.yaml` in this repo is copied directly from Speakeasy's published document, not hand-modeled.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/speakeasy-api/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/speakeasy-api/refs/heads/main/apis.yml)

## Why this entry exists

apis.io users searched for **API design**, **API lifecycle**, and **client library** and got zero results. Speakeasy sits squarely in that space: it turns an OpenAPI contract into client libraries across TypeScript, Python, Go, Java, C#, PHP, and more, and wires SDK generation into the API lifecycle through CI. This entry documents both the CLI/platform reality and the underlying public REST API.

## Tags

- API Lifecycle
- SDK Generation
- Client Library
- API Design
- Developer Tools
- OpenAPI
- Code Generation
- Terraform
- MCP
- Developer Experience

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## Authentication

The Speakeasy REST API accepts three credential types (see `authentication/`):

- `x-api-key` - a workspace API key header
- `x-workspace-identifier` - a workspace identifier header
- `Authorization: Bearer <token>` - a Bearer token

## APIs

The public Speakeasy API (OpenAPI 3.0.3, ~65 operations) is grouped below. All share base URL `https://api.prod.speakeasy.com`.

### Speakeasy API Registry (Artifacts) API

Manage versioned Registry artifacts - list namespaces, revisions, and tags, set visibility, archive namespaces, run preflight checks, and register remote sources. Includes OCI-compatible blob and manifest retrieval so OpenAPI specs and generated SDK artifacts can be pulled like container images.

- **Human URL:** [Publish specs to the API registry](https://www.speakeasy.com/guides/openapi/publish-specs-to-api-registry)
- **Base URL:** `https://api.prod.speakeasy.com`

### Speakeasy Workspaces API

Create and manage workspaces (the tenancy that owns SDK targets and generation config) - details, settings, team and per-user access, workspace tokens, and feature flags.

### Speakeasy Organizations API

Manage organizations (the tenancy above workspaces) - create organizations, read details and usage, start a free trial, and manage billing add-ons.

### Speakeasy Schema Store API

Store and retrieve OpenAPI specifications (JSON or YAML) keyed by package name and SDK class name - the backing store for turning a spec into a generatable API definition.

### Speakeasy Code Samples API

Retrieve and preview usage snippets generated from a Speakeasy SDK - per-operation client-library code samples in each generated language, with a synchronous preview and an async job flow.

### Speakeasy Generation Events API

Record and search events captured by a Speakeasy binary (CLI and GitHub Action) - each SDK generation, publish, and lint run, per workspace and per target - an audit trail of the SDK lifecycle.

### Speakeasy Reports API

Upload and retrieve OpenAPI lint reports and change (diff) reports as signed URLs keyed by document checksum, supporting API governance and safe spec evolution.

### Speakeasy GitHub Automation API

Drive the GitHub integration - check access, configure generation targets and docs/code-sample repos, store publishing secrets, trigger the Speakeasy Action, and inspect publishing PRs.

### Speakeasy Suggest (OpenAPI AI) API

LLM-powered OpenAPI improvement suggestions - propose fixes to an OpenAPI document from a full spec, a summary, or a registry revision, to raise API design quality before generation.

### Speakeasy Auth API

Exchange and validate credentials - get an access token, validate a workspace API key, read the authenticated user, and check workspace access.

### Speakeasy Publishing Tokens API

Create, read, update expiration, and delete publishing tokens used to publish generated SDKs to package registries.

### Speakeasy Subscriptions API

Manage subscriptions to CLI and registry events - activate or ignore a subscription for a given registry namespace.

## Pricing (summary)

- **Free** - $0. 250 operations per language, 1 language license, community Slack support.
- **Business** - $720/month ($600/month billed annually), licensed **per language**. OAuth, webhooks, SSE, docsite integration; 250 operations per language.
- **Enterprise** - custom pricing. Dedicated support, concierge onboarding, SLAs, SSO, audit logs.

An operation is a single GET/POST/PATCH/DELETE in your API interface; SDKs for the same language share one operation limit. New accounts get a 14-day Business trial. See `plans/` and `finops/`.

## Common Properties

- [GitHub Organization](https://github.com/speakeasy-api)
- [LinkedIn](https://www.linkedin.com/company/speakeasyapi)
- [Website](https://www.speakeasy.com)
- [Documentation](https://www.speakeasy.com/docs)
- [Plans](plans/speakeasy-api-plans-pricing.yml)
- [Rate Limits](rate-limits/speakeasy-api-rate-limits.yml)
- [Fin Ops](finops/speakeasy-api-finops.yml)
- [Blog](https://www.speakeasy.com/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
