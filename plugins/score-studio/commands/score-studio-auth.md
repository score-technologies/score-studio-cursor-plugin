---
name: score-studio-auth
description: Sign in or out of the Score Studio MCP CLI using OAuth or an API key.
---

# Manage Score Studio authentication

Determine whether the user wants to sign in, replace an existing credential, or
sign out. Confirm that the `score-studio-mcp` executable is available before
running a command.

For sign-in, run:

```bash
score-studio-mcp auth login
```

Let the CLI present its OAuth or API-key choice. Prefer browser OAuth for an
interactive user, and allow them to complete the browser consent flow. Do not
ask them to paste credentials into chat and never print or inspect the persisted
credential. When executing the MCP server from its source checkout, use
`npm start -- auth login` instead.

For sign-out, run:

```bash
score-studio-mcp auth logout
```

When executing from source, use `npm start -- auth logout`. Report whether the
operation succeeded, but do not reveal credential contents or storage details.
