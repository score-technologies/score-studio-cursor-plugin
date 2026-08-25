# Score Studio capability map

Use this public capability map to choose a product path, not to hardcode an API.
Verify the current SDK, OpenAPI contract, and block catalog before
implementation.

## Core lifecycle

| Area | What developers can automate | Important invariant |
| --- | --- | --- |
| Data | Create datasets, ingest media, import/export annotations, inspect health, archive/restore, create versions | Training and evaluation pin immutable versions |
| Annotation | Specialist labels plus VLM captions, questions, answers, phrases, and linked regions; auto-label, durable counts, provenance, and human review | Teacher output is proposed evidence; empty output is not successful labeling |
| Models | Registry discovery, specialist training, evidence-gated auto-training, VLM fine-tuning, calibration, artifacts/weights | Artifact export is not improvement; preserve phases, verdict, independent evaluation, and model-version provenance |
| Evaluation | Contract validation, saved profiles, measured runs, real progress, cancel/retry, reports, intervals, calibration, class/size slices, segmentation metrics, leaderboard and conformity | Only identical comparison keys are ranked; release uses the exact eligible run ID |
| Workflows | Typed graph of inputs, models/VLMs, transformations, logic, training, evaluation, release, monitoring, and integrations | Definition, preview, workload, and deployment are distinct states |
| Production | Managed/provider/edge deployment, revisions, exact-run release, verification, rollback, inference, logs, devices, monitoring, captured samples | Model, runtime, provider, credentials, and storage are separate; retain active-revision health evidence |
| Operations | Durable workloads and global task controls | Only expose pause/resume/cancel when the task state permits it |
| Platform | Organizations and member administration, API keys, providers, usage/billing, Stripe/TAO/alpha payments, audit, SSO/SCIM | Scope access to the organization and least privilege; production config fails closed |

## Current Python SDK surface

The bundled SDK baseline exposes methods for:

- `login`, `me`, and `orgs`;
- `datasets`, `dataset`, `create_dataset`, dataset versions, and image upload;
- `models`, `model`, model versions, `train`, estimates, and bounded wait;
- evaluation list/start/detail/report/wait and leaderboard;
- deployment list/detail/create/delete, `predict`, and sandbox inference;
- competition briefs, submissions, and acceptance;
- API-key list/create/revoke.

Inspect the installed package for exact signatures. Newer REST capabilities may
not yet have a matching SDK helper.

## REST capabilities ahead of the SDK

The 2026-08-25 OpenAPI contract adds operations for:

- validating an evaluation contract before queueing;
- creating/listing immutable evaluation profiles and running a profile;
- canceling an active evaluation or retrying failed/canceled evidence as a new
  run;
- releasing the exact eligible evaluation run rather than searching history;
- verifying deployment health with retained runtime/provider/device evidence;
- rolling back a deployment revision, using provision-verify-switch-release for
  provider runtimes that cannot mutate in place;
- checking segmentation runtime readiness;
- removing organization members with owner/admin boundaries;
- inspecting alpha payment addresses, deposits, and burns.

Verify exact paths and schemas in the current OpenAPI document.

## Measured evaluation surface

Contract v3 supports detection, classification, and segmentation. Depending on
task and available evidence it reports mAP50/mAP50–95, precision, recall, F1,
accuracy, per-class evidence, confusion, object-size slices, threshold sweeps,
calibration, deterministic bootstrap intervals, latency, throughput, CPU/memory,
and visible NVIDIA GPU/power/energy telemetry. Segmentation adds instance-mask
AP, matched mask IoU, Dice, and Boundary IoU. Never invent unavailable remote
resource telemetry.

## Workflow block families

The current catalog includes:

- inputs: uploaded image, immutable dataset version, camera/stream;
- specialist inference and VLM inference;
- confidence/class filters, counts, branches, crops, resize, rotation, merges;
- annotation interchange, auto-label, and human review;
- fine-tuning and preference/RL optimization;
- evaluation runs, conformity rounds, and evaluation gates;
- cloud and edge targets;
- monitoring, captured samples, and vision events;
- webhook, object-storage, and MQTT sinks.

Catalog entries declare ports, value types, required fields, visibility rules,
and runtime class. Fetch those declarations instead of reproducing them from
memory.

## Choosing a path

- Use a registry model when it meets the proof standard without adaptation.
- Train a specialist model for narrow, stable detection/segmentation/
  classification outputs.
- Use or fine-tune a VLM when language and grounded reasoning are part of the
  required output.
- Use Model Foundry when existing models and adaptation paths cannot credibly
  meet the evaluation contract.
- Use a workflow only when orchestration, branching, multiple models, release
  gates, integrations, or feedback loops add real value.
