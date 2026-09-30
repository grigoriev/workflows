# Contributing

Issues and pull requests are welcome.

## Build and test

```sh
docker run --rm -v "$PWD":/repo -w /repo rhysd/actionlint
docker run --rm -v "$PWD":/repo -w /repo ghcr.io/zizmorcore/zizmor --min-severity low .
uv run --no-project --with pyyaml .github/scripts/check_tool_list_parity.py .github/workflows/*.yml
```

CI runs the same three checks for every pull request.

## Pull requests

1. Branch from the default branch as `type/description`, for example `fix/review-prompt`.
2. Keep one change per pull request.
3. Write commit messages as [Conventional Commits](https://www.conventionalcommits.org/) without a
   scope: `feat: ...`, `fix: ...`, `docs: ...`, `refactor: ...`, `test: ...`, `build: ...`,
   `ci: ...`, `chore: ...`.
4. Sign your commits. The default branch accepts verified signatures only.
5. Add an entry under `## [Unreleased]` in `CHANGELOG.md`, written for users. Update the
   README when behavior changes.

Pull requests are squash-merged once all required checks are green.

## Releases

The workflows have no releases. Callers pin a commit of `main`, and Renovate moves the pin.
