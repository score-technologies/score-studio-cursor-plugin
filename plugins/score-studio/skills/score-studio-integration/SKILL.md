---
name: score-studio-integration
description: Integrate an application with Score Studio's SDK or REST API across datasets, training, evaluation, deployment, inference, competitions, and API keys. Use when adding or debugging Score Studio client code.
---

# Score Studio integration

Read `../../references/capability-map.md` and
`../../references/contract-playbook.md` before implementing.

## Contract discovery

Use the first available source:

1. imported or installed `scorestudio` package source and version;
2. a repository OpenAPI document or generated client;
3. an authorized live `/openapi.json` document;
4. the bundled reference, only for planning.

Search for existing client wrappers, configuration, authentication, retries,
polling, telemetry, and test fixtures. Extend local conventions instead of
creating a second integration stack.

## Implementation loop

1. Name the single user outcome being implemented.
2. Map it to verified client methods or endpoints and response schemas.
3. Define typed application-level inputs and outputs so vendor payloads do not
   leak through the whole codebase.
4. Read URL/token configuration from secrets. Do not log tokens, API keys,
   signed URLs, raw private media, or provider credentials.
5. Set explicit request timeouts. For long-running operations, use bounded
   polling with terminal states and preserve the durable task/run identifier.
6. Preserve provenance identifiers: organization, dataset slug and version,
   model and model version, evaluation run, workflow, workload, deployment and
   revision as applicable.
7. Translate Score Studio errors into actionable application errors while
   retaining status and machine-readable error code.
8. Test success, authorization failure, validation failure, timeout, and the
   relevant terminal failure state with transport-level fakes.

## Python SDK baseline

The 2026-08-24 SDK exposes the core loop: login/orgs; dataset creation,
versioning, and uploads; model listing and training; evaluation and leaderboard;
deployment and inference; competitions; and API-key management. Method names in
the bundled capability map are hints only. Inspect the installed client before
calling them.

## Done when

- the implementation uses a verified contract;
- secrets stay outside source control;
- async work cannot poll forever;
- immutable version identifiers are preserved;
- errors and preview/deferred behavior remain truthful;
- focused tests pass and the usage path is documented.
