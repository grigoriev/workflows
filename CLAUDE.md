# workflows

Reusable GitHub Actions workflows, called from the repositories under github.com/grigoriev.

- `claude-review.yml` derives from
  SchweizerischeBundesbahnen/github-workflows-polarion (Apache-2.0). Keep the NOTICE current.
- `claude-code-review.yml` is the caller of this repository.
- Pin every action by SHA with a version comment.
- `settings.permissions.allow` and `--allowedTools` in `claude-review.yml` must hold the same
  tools. `check_tool_list_parity.py` asserts it in CI.
- A change here reaches every caller through a Renovate pull request. Keep inputs backward
  compatible.

Checks: see CONTRIBUTING.md. Conventions: CONTRIBUTING.md, Conventional Commits without a scope.
