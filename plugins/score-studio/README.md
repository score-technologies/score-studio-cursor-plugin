# Score Studio

## Give your agents sight.

Score Studio is the computer vision layer for agents, automating data
generation, annotation, training, evaluation, workflows, and deployment in one
evidence-backed system.

Score Studio for Cursor brings that whole vision lifecycle into the codebase
you already have: data → model or VLM → evidence → workflow → runtime →
production feedback.

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
- `/score-studio-auth`: sign in or out with the Score Studio MCP CLI.
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

No API credential is stored by this plugin. The Score Studio MCP CLI persists
its own credential after an interactive browser OAuth login or API-key login.
Starting the CLI prompts for one of those methods when no saved credential is
available. You can also manage the session explicitly:

```bash
score-studio auth login
score-studio auth logout
```

When running this repository's MCP server from source, use `npm run auth` or
`npm run auth:logout`. OAuth is preferred for
interactive use; API keys and `SCORESTUDIO_TOKEN` remain suitable for CI and
other non-interactive secret stores. Never commit credentials. The production
API defaults to `https://api.scorestudio.ai`; set `SCORESTUDIO_URL` only for a
custom, staging, self-hosted, or local Score Studio API.

## Contract policy

The bundled capability map is a planning aid, not a frozen API specification.
Before generating integration code, the agent checks, in order:

1. the current repository's installed `scorestudio` SDK;
2. a checked-in Score Studio OpenAPI document or generated client;
3. the live deployment's OpenAPI document, when the user authorizes access;
4. the bundled reference only when none of the above is available.

This prevents an older plugin release from inventing endpoints or fields.
