# Contributing

Bug reports and pull requests are welcome. For a larger change, open an issue first so we can agree on the approach before you write it.

## Setup

The extension is one Bash script with no build step.

```bash
git clone <your-fork-url> gh-current-pr && cd gh-current-pr
gh extension install .        # run your checkout as `gh current-pr`
```

Edits to `gh-current-pr` take effect on the next run. To test against a real PR, run it from any repository whose current branch has an open pull request.

## Before you open a pull request

- `shellcheck gh-current-pr` passes. CI runs the same check.
- `bash -n gh-current-pr` passes, and `./gh-current-pr --help` prints the usage text.
- The script still runs on macOS (BSD tools, Bash 3.2) and Linux (GNU tools). Avoid GNU-only flags for `sed`, `date`, and `grep`.
- README and `--help` match any flag or output change.
- `CHANGELOG.md` has an entry under `Unreleased`.

## Reporting a bug

Include the `gh --version` and `jq --version` output, your OS, the command you ran, and the full output. If the wrong PR was picked, add the output of `git remote -v` and `git rev-parse --abbrev-ref @{upstream}`, with private remote URLs redacted.
