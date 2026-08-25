# Score Studio for Cursor

## Give your agents sight.

Score Studio is the computer vision layer for agents, automating data
generation, annotation, training, evaluation, workflows, and deployment in one
evidence-backed system.

This Cursor plugin turns a computer-vision objective into a versioned,
evidence-gated Score Studio system. It helps an agent inspect the live contract,
integrate the Python SDK or REST API, compose workflows, and check a model or
workflow before release.

The plugin was built from Cursor's official plugin template and is intentionally
focused on the parts of Score Studio that are useful from a codebase:

- data ingestion, annotation interchange, versioning, and health;
- specialist model training and VLM fine-tuning;
- contract-v3 evaluation, reproducible evidence, and release gates;
- workflow composition across models, logic, deployment, and monitoring;
- deployment, inference, workloads, and the production feedback loop.

See [the plugin README](plugins/score-studio/README.md) for commands and local
installation.

## Validate

```bash
node scripts/validate-template.mjs
```

The plugin is licensed under Apache-2.0. Test each release as a local plugin in
Cursor before publishing or refreshing its marketplace listing.

## Compatibility

The plugin contains public product guidance for the current Score Studio API,
SDK, workflows, evaluation methodology, and runtime evidence boundaries. It
tells Cursor to prefer a project's installed SDK and live OpenAPI document over
bundled guidance whenever they differ.
