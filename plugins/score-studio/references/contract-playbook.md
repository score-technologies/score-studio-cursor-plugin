# Contract playbook

## Source-of-truth order

1. Installed SDK source and version for code that uses the SDK.
2. Checked-in OpenAPI artifact or generated client.
3. Authorized live OpenAPI document for the target deployment.
4. This plugin's capability map for planning only.

Record which source and version were used in the change or handoff.

## Integration boundaries

Wrap Score Studio behind an application-owned client or service boundary. Keep
vendor request/response objects at that edge and return domain-specific values
to the rest of the application.

Preserve identifiers needed for audit and idempotency:

- organization slug;
- dataset slug and immutable version number/id;
- model slug/id and model version id;
- evaluation profile id, exact evaluation run id, frozen comparison key, and
  benchmark version;
- workflow slug/version and workload/task id;
- deployment slug, revision, and runtime/provider identity.

## Authentication

The interactive Score Studio MCP CLI should use its persisted browser OAuth
session (`score-studio-mcp auth login`) by default, with API-key login as the
fallback and `score-studio-mcp auth logout` removing the saved credential. The
Python SDK baseline accepts `token=` or `SCORESTUDIO_TOKEN` and accepts its API
through `base_url=` or `SCORESTUDIO_URL`; these remain appropriate for CI and
other non-interactive secret stores. Generated hosted integrations should fall
back to `https://api.scorestudio.ai` when neither URL override is set.
Inference may use a scoped API key. Verify current scope names before creating
a key. A key value may be shown only once; send it directly to the deployment
secret store and never log it.

## Durable operations

Training, auto-generation, annotation, evaluation, media processing, and
provider-backed work can be durable jobs. Store the returned identifier, poll
with a deadline and backoff, expose completed/total progress, stop on documented
terminal states, and map task capabilities instead of assuming every running
task can be paused or cancelled. When supported, send an idempotency key.
Cancel only queued/leased/running evaluations; retry only failed/canceled runs,
and preserve the original evidence.

## Evaluation API baseline

The current REST surface validates contracts, saves/lists evaluation profiles,
runs profiles, creates/lists/gets evaluations, controls cancel/retry, and returns
report and evidence artifacts. Validation returns `ready`, the normalized frozen
contract, errors, and warnings. Run responses include task, evaluator revision,
state, seed, normalized metric config, progress, attempts, and failure code.

Use the exact evaluation run ID for automatic release. Do not search historical
runs in client code or select the highest score after the fact.

## Workflow API baseline

The current REST surface can list templates and blocks, list/create/get/update/
delete workflows, and run a workflow against an image object key. A run response
contains outputs, detection count, mode, and deferred blocks. Verify route paths
and schemas from the current contract before use.

## Deployment API baseline

After creation or revision activation, call the verified deployment-health
operation and retain provider, status, checked time, revision ID, evidence event
ID, and resource evidence. Rollback requires a previous revision. For connected
compute/inference providers, rollback may provision and verify a replacement
before switching; failed replacement must leave the current revision active.

## Error policy

Preserve HTTP status, machine code, and safe message. Differentiate:

- invalid caller input;
- authentication/authorization failure;
- missing organization resource;
- incompatible model/runtime/provider;
- unavailable optional integration;
- durable job failure or timeout;
- evaluation contract errors versus non-blocking statistical/provenance warnings;
- incomparable evaluation protocols;
- unhealthy or degraded active revisions;
- preview/deferred work that has not executed.
