# Security policy

## Reporting a vulnerability

Report a vulnerability privately through GitHub:
https://github.com/grigoriev/workflows/security/advisories/new
(the **Security** tab, **Report a vulnerability**). Do not open a public issue for it.

We answer within a week. The fix goes to `main`, and the CHANGELOG names it.

## Supported versions

Only `main` gets fixes. Callers pin a commit of `main`, and Renovate moves the pin.

## Scope

The reusable workflows, the callers of this repository and the check script.

Vulnerabilities in `anthropics/claude-code-action` or in Claude Code belong to the upstream
project. Tell us as well if these workflows are affected, so we can change them.
