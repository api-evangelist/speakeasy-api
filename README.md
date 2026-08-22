# Speakeasy (speakeasy-api)

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
