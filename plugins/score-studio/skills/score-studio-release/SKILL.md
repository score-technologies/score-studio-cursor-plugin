---
name: score-studio-release
description: Assess whether a Score Studio model, workflow, or deployment is ready for production using evaluation evidence, conformity, compatibility, security, observability, and feedback-loop checks.
---

# Score Studio release readiness

Read `../../references/release-gates.md`. Inspect real evidence from the current
repository and, when authorized, Score Studio. Do not infer a pass from UI copy,
demo data, a successful build, or the existence of a deployment record.

## Procedure

1. Identify the exact release candidate: model version or workflow version,
   deployment revision, intended runtime, and environment.
2. Resolve the evaluation contract and immutable benchmark version.
3. Verify metric results, class/slice failures, visual evidence, latency, and any
   conformity policy. A missing required result is a block.
4. Verify artifact availability and compatibility: runnable weights, format,
   provider/device capability, storage, and capacity.
5. Verify secrets and access: least-privilege API key scopes, no checked-in
   credentials, authenticated provider connection, and organization isolation.
6. Verify operational controls: durable job state, timeouts, pause/resume/cancel
   truth, logs, monitoring, alerts or review ownership, and rollback path.
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
