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
- evaluation run id and benchmark version;
- workflow slug/version and workload/task id;
- deployment slug, revision, and runtime/provider identity.

## Authentication

The Python SDK baseline accepts `token=` or `SCORESTUDIO_TOKEN` and reads
`SCORESTUDIO_URL`. Inference may use a scoped API key. Verify current scope names
before creating a key. A key value may be shown only once; send it directly to
the deployment secret store and never log it.

## Durable operations

Training, auto-generation, annotation, evaluation, media processing, and
provider-backed work can be durable jobs. Store the returned identifier, poll
with a deadline and backoff, stop on documented terminal states, and map task
capabilities instead of assuming every running task can be paused or cancelled.

## Workflow API baseline

The current REST surface can list templates and blocks, list/create/get/update/
delete workflows, and run a workflow against an image object key. A run response
contains outputs, detection count, mode, and deferred blocks. Verify route paths
and schemas from the current contract before use.

## Error policy

Preserve HTTP status, machine code, and safe message. Differentiate:

- invalid caller input;
- authentication/authorization failure;
- missing organization resource;
- incompatible model/runtime/provider;
- unavailable optional integration;
- durable job failure or timeout;
- preview/deferred work that has not executed.
