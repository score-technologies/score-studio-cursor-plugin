# Security policy

## Reporting a vulnerability

Report vulnerabilities privately through [GitHub Security Advisories](https://github.com/score-technologies/score-studio-cursor-plugin/security/advisories/new). Do not disclose credentials, customer data, or exploit details in a public issue.

## Public-release boundary

This repository contains only public Cursor plugin guidance and manifests. It
must not contain private source-repository identifiers, private source commit
identifiers, local filesystem paths, credentials, customer data, or symlinks.
The release validator enforces this boundary.

Keep Score Studio URLs and credentials in local environment configuration or a
secret manager. Never embed them in plugin content, prompts, rules, or source
control.
