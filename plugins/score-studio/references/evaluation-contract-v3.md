# Evaluation contract v3

This document describes the public contract-v3 behavior. Verify the live
OpenAPI schema and evaluator revision before implementation.

## Evidence identity

One evaluation measures one exact executable model version against one exact
immutable dataset version. Its frozen contract includes purpose, distribution,
split, label schema/mapping, thresholds, slices, maximum samples, random seed,
evaluator digest/revision, provenance, manifest counts, and acceptance criteria.

Validate the contract before queueing. Treat validation errors as blockers and
retain warnings. Saved evaluation profiles freeze the normalized contract and
can be rerun with a recorded seed and idempotency key.

## Data validity

- Test, benchmark, stress, and OOD purposes require a non-empty held-out split;
  `all` data is not acceptable.
- Model and dataset task types must match.
- When label schemas differ, provide a complete model-class-to-dataset-class
  mapping. Never reinterpret class IDs silently.
- Production validation uses labeled, non-archived dataset-file rows rather than
  trusting aggregate counters.
- Empty detection images remain in the denominator so false positives count.
- Invalid or missing media/annotations stop the run. Current bounds are 100 MB
  per image, 10 MB per annotation document, 10,000 annotations per image, and
  268 million declared pixels.
- Fewer than 30 selected images produces a statistical warning, not a universal
  adequacy verdict.

## Measured results

Detection reports mAP50, mAP50–95, precision, recall, F1, per-class AP,
confusion, and small/medium/large object slices when dimensions exist.
Classification reports accuracy, precision, recall, F1, per-class results, and
a confusion matrix. Segmentation reports instance-mask AP50/AP50–95, matched
mask IoU, Dice, and Boundary IoU using a two-percent image-relative contour
tolerance.

Reports may also include a confidence-threshold sweep, ten-bin expected
calibration error, deterministic image-level bootstrap 95% intervals, sample
progress, single-sample/p95 latency, wall/CPU time, peak memory, throughput, and
visible NVIDIA GPU utilization, memory, power, and energy.

Never substitute an advertised provider rate for measured billing, or infer
remote GPU/energy values when no provider or worker sensor exposes them.

## Comparability

Only compare runs with identical comparison keys: task, purpose, distribution,
split, metric scope, thresholds, sample cap, class scope/mapping, evaluator
digest/revision, and seed. Report excluded incompatible runs instead of ranking
them together.

Bootstrap intervals cover sampling variation in evaluated images, not label
error, domain shift, training variance, or dependency changes. Latency without
warmup is suitable only for comparisons using the same runtime protocol.

## Release eligibility

Automatic release requires all of:

1. a succeeded, measured contract-v3 run;
2. benchmark or held-out in-distribution test evidence;
3. verified labeled-file manifest and dataset source provenance;
4. a recorded license when using benchmark evidence;
5. passing acceptance criteria declared before execution;
6. the exact evaluated artifact in ready state.

Validation, stress, and OOD evidence remain useful but cannot independently
authorize release. Pass the exact evaluation run ID to release; never search for
a more favorable historical score.

## Durable controls and reproducibility

Runs retain progress, attempts, failure code, seed, evaluator identity, frozen
contract, sample manifest hash, prediction hash, timestamps, result schema, and
artifact identity. Cancel only active work. Retry only failed/canceled work and
create a new run so the original evidence remains immutable. Use idempotency keys
to avoid accidental duplicate queueing.
