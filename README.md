# Score Studio for Cursor

A Cursor plugin for turning a computer-vision objective into a versioned,
evidence-gated Score Studio system. It helps an agent inspect the live contract,
integrate the Python SDK or REST API, compose workflows, and check a model or
workflow before release.

The plugin was built from Cursor's official plugin template and is intentionally
focused on the parts of Score Studio that are useful from a codebase:

- data ingestion, annotation interchange, versioning, and health;
- specialist model training and VLM fine-tuning;
- evaluation, conformity evidence, and release gates;
- workflow composition across models, logic, deployment, and monitoring;
- deployment, inference, workloads, and the production feedback loop.

See [the plugin README](plugins/score-studio/README.md) for commands and local
installation.

## Validate

```bash
node scripts/validate-template.mjs
```

The plugin is licensed under Apache-2.0. Before marketplace submission, add the
final repository URL to the plugin manifest and test the installed plugin in
Cursor.

## Source baseline

Product guidance was derived from Score Studio commit `08bc450` (2026-08-24),
including the current OpenAPI contract, Python SDK, workflow block catalog, and
launch-readiness audit. The plugin tells Cursor to prefer a project's installed
SDK and live OpenAPI document over this bundled snapshot whenever they differ.
