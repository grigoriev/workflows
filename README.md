# workflows

[![CI](https://github.com/grigoriev/workflows/actions/workflows/ci.yml/badge.svg)](https://github.com/grigoriev/workflows/actions/workflows/ci.yml)
[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/grigoriev/workflows/badge)](https://scorecard.dev/viewer/?uri=github.com/grigoriev/workflows)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

Reusable GitHub Actions workflows for the repositories under
[grigoriev](https://github.com/grigoriev).

| Workflow | Purpose |
|---|---|
| [`claude-review.yml`](.github/workflows/claude-review.yml) | Claude Code reviews a pull request once, when it opens or becomes ready |

It derives from
[SchweizerischeBundesbahnen/github-workflows-polarion](https://github.com/SchweizerischeBundesbahnen/github-workflows-polarion),
see [NOTICE](NOTICE).

## Usage

The calling repository needs the secret `CLAUDE_CODE_OAUTH_TOKEN` (`claude setup-token`)
and the [Claude GitHub App](https://github.com/apps/claude).

`.github/workflows/claude-code-review.yml`:

```yaml
---
name: Claude Code Review
on:
  pull_request:
    types: [opened, ready_for_review, reopened]
concurrency:
  group: claude-review-${{ github.event.pull_request.number }}
  cancel-in-progress: true
permissions: {}
jobs:
  claude-review:
    uses: grigoriev/workflows/.github/workflows/claude-review.yml@<sha> # main
    permissions:
      actions: read
      contents: read
      pull-requests: write
      issues: write
      id-token: write
    secrets:
      CLAUDE_CODE_OAUTH_TOKEN: ${{ secrets.CLAUDE_CODE_OAUTH_TOKEN }}
```

1. Pin a commit of `main` by SHA. The repositories require SHA pinning.
2. Renovate moves the pin after each merge here.
3. Add `with: extra_focus: <text>` to the review call for a repository-specific focus.

The review runs once per pull request. Re-run the job for a further round. The review
skips drafts, fork pull requests and bot pull requests. It reads `CLAUDE.md` of the calling
repository for the project conventions.

The review is advisory. Do not make it a required check: Renovate pull requests skip it.

## Known limitations

- **A pull request that edits a caller workflow gets no review.** `claude-code-action`
  requires the caller file to match the default branch. Otherwise the action skips the
  review and the job still ends green. A change of the reusable workflow alone is reviewed.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Report vulnerabilities privately, see
[SECURITY.md](SECURITY.md).

## Disclaimer

These workflows are provided "as is", without warranty of any kind, as the
[LICENSE](LICENSE) states. Use them at your own risk. Sergey Grigoriev is not liable for
damage from their use, as far as the law allows. They are published free of charge,
outside of any commercial offering, with no obligation to support them. Security reports
are welcome, see [SECURITY.md](SECURITY.md).

## License

Apache 2.0, see [LICENSE](LICENSE) and [NOTICE](NOTICE).
