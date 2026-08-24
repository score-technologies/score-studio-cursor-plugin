# Release gates

Use the applicable gates. Mark an inapplicable gate explicitly; do not silently
drop it.

| Gate | Required evidence |
| --- | --- |
| Candidate identity | Exact model/workflow version and deployment revision |
| Evaluation contract | Immutable benchmark, output schema, metrics, thresholds, slices, and latency target |
| Quality | Completed run, aggregate and slice metrics, visual/hard-example review, failure analysis |
| Conformity | Completed required policy profile and auditable result |
| Artifact | Runnable weights/artifact, checksum or version identity, supported format |
| Runtime compatibility | Model task and format supported by selected managed/provider/edge runtime |
| Provider/device | Tested connection, capacity, region/device identity, and failure behavior |
| Security | Least-privilege key, secrets out of source, organization isolation, safe media handling |
| Execution truth | No deferred/preview block represented as executed production work |
| Reliability | Durable state, bounded retries/polling, timeouts, idempotency where needed, rollback |
| Observability | Logs, metrics, latency/volume/error monitoring, owner and response path |
| Feedback | Sampling policy, retention/privacy, review queue, new-version promotion path |
| Cost | Expected training/inference/storage usage and an accepted budget or limit |

## Severity

- Block release for missing mandatory evaluation, failed quality threshold,
  incompatible artifact/runtime, leaked or absent required credentials,
  unbounded execution, or misleading preview state.
- Use conditional only for an explicit deploy-time dependency with an owner and
  verification step.
- A passing build or smoke request is supporting evidence, not a substitute for
  the evaluation contract.
