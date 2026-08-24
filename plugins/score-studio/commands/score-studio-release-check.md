---
name: score-studio-release-check
description: Audit a Score Studio model or workflow against evidence, runtime, security, and operability gates before release.
---

# Check a Score Studio release

Load the `score-studio-release` skill and inspect the current integration and
available Score Studio evidence.

Return one of: `ready`, `conditional`, or `blocked`. Every failed or unknown gate
must include the evidence inspected, the missing proof, impact, and the smallest
next action. Never convert an unavailable provider, missing credentials,
preview-only workflow block, or absent evaluation result into a pass.
