# Release gates

Use the applicable gates. Mark an inapplicable gate explicitly; do not silently
drop it.

| Gate | Required evidence |
| --- | --- |
| Candidate identity | Exact model/workflow version and deployment revision |
| Evaluation contract | Contract v3; explicit purpose/distribution; non-empty held-out split; immutable dataset; provenance/license; output and class mapping; metrics, thresholds, slices, cap, seed, evaluator and acceptance criteria |
| Eligible release evidence | Exact succeeded measured run; benchmark or held-out in-distribution test; verified labeled manifest; passing predeclared criteria; exact ready artifact |
| Quality | Aggregate/class/size metrics, threshold sweep, calibration, intervals, confusion, visual/hard-example review, failure analysis |
| Conformity | Completed required policy profile and auditable result |
| Artifact | Runnable weights/artifact, checksum or version identity, supported format |
| Runtime compatibility | Model task and format supported by selected managed/provider/edge runtime |
| Provider/device | Tested connection, capacity, region/device identity, active-revision acknowledgement, retained health event, and failure behavior |
| Security | Least-privilege key, secrets out of source, organization isolation, safe media handling |
| Execution truth | No deferred/preview block represented as executed production work |
| Reliability | Durable state and measured progress, bounded retries/polling, valid cancel/retry controls, timeouts, idempotency, verified rollback |
| Observability | Logs, metrics, latency/volume/error and available resource/cost monitoring, evidence event IDs, owner and response path |
| Feedback | Sampling policy, retention/privacy, review queue, new-version promotion path |
| Cost | Expected training/inference/storage usage and an accepted budget or limit |

## Severity

- Block release for a non-v3, unmeasured, validation/stress/OOD-only, leaky,
  unlicensed benchmark, incomparable, or failed mandatory evaluation; a failed
  quality threshold;
  incompatible artifact/runtime, leaked or absent required credentials,
  unbounded execution, an unacknowledged active revision, or misleading preview
  state.
- Use conditional only for an explicit deploy-time dependency with an owner and
  verification step.
- A passing build or smoke request is supporting evidence, not a substitute for
  the evaluation contract.
