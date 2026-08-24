# Score Studio capability map

Baseline: Score Studio `08bc450`, 2026-08-24. Use this to choose a product path,
not to hardcode an API. Verify the current SDK, OpenAPI contract, and block
catalog before implementation.

## Core lifecycle

| Area | What developers can automate | Important invariant |
| --- | --- | --- |
| Data | Create datasets, ingest media, import/export annotations, inspect health, archive/restore, create versions | Training and evaluation pin immutable versions |
| Annotation | Specialist labels plus VLM captions, questions, answers, phrases, and linked regions; auto-label and human review | Uncertain output remains reviewable evidence |
| Models | Registry discovery, specialist training, VLM fine-tuning, calibration, artifacts/weights | Preserve model-version provenance |
| Evaluation | Runs, reports, visual evidence, class/slice analysis, leaderboard, conformity and monitoring | Release gates name a dataset version, metric, threshold, and result |
| Workflows | Typed graph of inputs, models/VLMs, transformations, logic, training, evaluation, release, monitoring, and integrations | Definition, preview, workload, and deployment are distinct states |
| Production | Managed/provider/edge deployment, revisions, actions, inference, logs, devices, monitoring, captured samples | Model, runtime, provider, credentials, and storage are separate choices |
| Operations | Durable workloads and global task controls | Only expose pause/resume/cancel when the task state permits it |
| Platform | Organizations, API keys, providers, usage/billing, audit, SSO/SCIM | Scope access to the organization and least privilege |

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
