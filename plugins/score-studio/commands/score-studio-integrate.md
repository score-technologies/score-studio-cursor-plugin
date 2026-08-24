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

Keep authentication in environment or the application's secret store. Add
typed boundaries, actionable API errors, timeouts, bounded polling for durable
jobs, and tests with network calls mocked at the transport boundary. Verify the
changed path without running unrelated destructive operations.

Report the exact contract source used and any Score Studio operations that
remain intentionally unimplemented.
