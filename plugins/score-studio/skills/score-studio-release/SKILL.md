---
name: score-studio-release
description: Assess whether a Score Studio model, workflow, or deployment is ready for production using evaluation evidence, conformity, compatibility, security, observability, and feedback-loop checks.
---

# Score Studio release readiness

Read `../../references/release-gates.md` and
`../../references/evaluation-contract-v3.md`. Inspect real evidence from the
current repository and, when authorized, Score Studio. Do not infer a pass from
UI copy, demo data, a successful build, an exported artifact, or the existence
of a deployment record.

## Procedure

1. Identify the exact release candidate: model version or workflow version,
   deployment revision, intended runtime, and environment.
2. Resolve the frozen contract-v3 evaluation and immutable benchmark version.
   Verify that it is a held-out in-distribution test or benchmark with manifest,
   provenance, and—when used as benchmark evidence—a recorded license.
3. Verify measured results, acceptance criteria, comparison compatibility,
   intervals, class/size slices, calibration, confusion and hard-example
   evidence, latency/resources, and any conformity policy. A missing required
   result is a block; unavailable provider telemetry stays unavailable.
4. Verify artifact availability and compatibility: runnable weights, format,
   provider/device capability, storage, and capacity.
5. Verify secrets and access: least-privilege API key scopes, no checked-in
   credentials, authenticated provider connection, and organization isolation.
6. Verify operational controls: durable job state and real progress, timeouts,
   valid cancel/retry capabilities, logs, monitoring, alerts or review ownership,
   idempotency, and rollback path. Verify that the active runtime/provider/device
   acknowledged the exact revision and retain the health event ID.
7. Verify the feedback loop: sampled production evidence, privacy/retention,
   human review, and promotion into a new immutable dataset version.

## Verdict

Return:

- `ready` only when all required gates have evidence;
- `conditional` when explicitly accepted operational dependencies remain, such
  as production credentials that are intentionally injected at deploy time;
- `blocked` when a quality, compatibility, security, or truthfulness gate fails.

For each non-pass, include evidence inspected, impact, and the smallest next
action. Separate product limitations from environment/configuration gaps.
