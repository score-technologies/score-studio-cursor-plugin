---
name: score-studio-integrate
description: Implement a minimal end-to-end Score Studio SDK or REST integration in the current project.
---

# Integrate Score Studio

Load the `score-studio-integration` skill, inspect the codebase, and implement the
smallest requested vertical slice.

Before editing, identify the current contract source and the project's existing
HTTP, configuration, error, and test conventions. Prefer the Python
`scorestudio` SDK when it is available and fits the project; otherwise generate
REST calls from the current OpenAPI contract.

For interactive MCP CLI use, prefer `score-studio auth login` and its saved
OAuth session; do not require the user to manually acquire or paste a token when
browser login is available. Use API keys or environment credentials for CI and
other non-interactive secret stores. Add typed boundaries, actionable API
errors, timeouts, bounded polling for durable jobs, and tests with network calls
mocked at the transport boundary. Verify the changed path without running
unrelated destructive operations.

Report the exact contract source used and any Score Studio operations that
remain intentionally unimplemented.
