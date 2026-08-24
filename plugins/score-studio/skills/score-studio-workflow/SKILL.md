---
name: score-studio-workflow
description: Design and validate Score Studio workflows that combine data, specialist models or VLMs, typed logic, evaluation gates, deployment targets, monitoring, and feedback. Use for workflow definitions or visual orchestration.
---

# Score Studio workflow

Read `../../references/capability-map.md` and discover the current block catalog
from the Score Studio API or repository before authoring a definition.

## Design sequence

1. State the operational outcome and the output consumer.
2. Select an input block and define input ownership, media constraints, and
   sampling behavior.
3. Select the smallest compatible model path. Use specialist models for stable
   narrow outputs; use VLMs when language, grounding, captioning, VQA, or
   structured visual reasoning is intrinsic to the task.
4. Connect ports only when their declared types are compatible. Do not infer an
   adapter that the catalog does not expose.
5. Validate or normalize model output before downstream automation. Use a
   structured-output contract for VLM responses.
6. Insert evaluation, conformity, or explicit threshold gates before any
   release target.
7. Keep runtime choices explicit. Provider-backed blocks need a tested provider
   connection; edge targets need a registered compatible device.
8. Add monitoring and captured-sample review when production decisions can
   drift or fail silently.

## Execution truth

A saved workflow definition is not a completed workload. A preview response may
execute local image/model/logic blocks while returning provider-backed,
training, evaluation, deployment, or feedback blocks in `deferred_blocks`.
Always expose `mode` and deferred work to the caller.

## Validation

Check:

- every required port is connected once unless it permits multiple values;
- every required field is present and points to an accessible organization
  resource;
- the graph has no unintended cycle or orphaned release path;
- dataset and evaluation nodes pin immutable versions;
- model weights and runtime format are compatible with the target;
- provider, device, and storage connections are tested;
- output and event payloads have explicit schemas;
- the feedback path creates reviewable data and a new version.

Return the definition plus a short execution table: block, runtime, prerequisites,
executed in preview, and production owner.
