---
name: score-studio-plan
description: Turn a computer-vision objective into an implementation-ready Score Studio architecture and evidence contract.
---

# Plan a Score Studio system

Use the `score-studio-architect` agent and the bundled capability map.

Inspect the repository before asking questions. Produce:

1. the operating outcome and non-goals;
2. inputs, outputs, and a machine-readable output contract;
3. the immutable evaluation dataset, metrics, slices, thresholds, and latency
   target;
4. the selected model path and why it is the smallest credible option;
5. the data, training/fine-tuning, evaluation, workflow, deployment, monitoring,
   and feedback stages that are actually needed;
6. the current SDK/OpenAPI contracts that implementation must verify;
7. milestones, acceptance checks, risks, and rollback behavior.

Do not implement unless the user also asks for implementation.
