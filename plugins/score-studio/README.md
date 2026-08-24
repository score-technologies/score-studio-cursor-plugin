# Score Studio

Score Studio for Cursor helps you build the whole vision lifecycle from the
codebase you already have: data → model or VLM → evidence → workflow → runtime
→ production feedback.

## Included

- `score-studio-integration` skill: implement SDK or REST integrations against
  the current contract.
- `score-studio-workflow` skill: design typed workflows and distinguish locally
  executable blocks from deferred provider-backed orchestration.
- `score-studio-release` skill: audit evidence, runtime compatibility,
  credentials, observability, and feedback capture before release.
- `score-studio-architect` agent: turn an operating problem and proof standard
  into a concrete Score Studio architecture.
- `/score-studio-plan`: produce an implementation-ready system plan.
- `/score-studio-integrate`: implement a minimal end-to-end integration.
- `/score-studio-workflow`: design or update a workflow definition.
- `/score-studio-release-check`: check whether a model or workflow is ready to
  release.

## Local installation

From this repository:

```bash
mkdir -p ~/.cursor/plugins/local
ln -s "$(pwd)/plugins/score-studio" ~/.cursor/plugins/local/score-studio
```

Restart Cursor or run `Developer: Reload Window`, then confirm the Score Studio
skills, agent, and commands appear in Customize.

No API credential is stored by this plugin. Application code should read
`SCORESTUDIO_URL` and `SCORESTUDIO_TOKEN` from its normal secret-management
path. Never commit either value.

## Contract policy

The bundled capability map is a planning aid, not a frozen API specification.
Before generating integration code, the agent checks, in order:

1. the current repository's installed `scorestudio` SDK;
2. a checked-in Score Studio OpenAPI document or generated client;
3. the live deployment's OpenAPI document, when the user authorizes access;
4. the bundled reference only when none of the above is available.

This prevents an older plugin release from inventing endpoints or fields.
