# gh-current-pr

A GitHub CLI extension that displays pull request information for your current branch, including title, URL, merge status, and CI check status.

## Installation

Install with `gh`:

```bash
gh extension install rushi/gh-current-pr
```

Or manually:

```bash
mkdir -p ~/.local/share/gh/extensions/gh-current-pr
cd ~/.local/share/gh/extensions/gh-current-pr
curl -o gh-current-pr https://raw.githubusercontent.com/rushi/gh-current-pr/main/gh-current-pr
chmod +x gh-current-pr
```

## Usage

Run in any git repository with a pull request:

```bash
gh current-pr
```

Output shows:

- PR title
- PR URL
- Merge status (Draft, Ready to merge, Conflicts, Blocked, etc.)
- Last code review (author and timestamp)
- Failing checks (if any)
- In-progress checks (if any)

Example output:

```
Fix login redirect on OAuth callback
https://github.com/owner/repo/pull/42
Merge: Conflicts
Last review: alice at Mar 16, 2026 01:00 PM
In progress:
  - Unit Tests
```

## Flags

`--url`

Print only the PR URL:

```bash
gh current-pr --url
# https://github.com/owner/repo/pull/42
```

Pipe it to other commands:

```bash
open $(gh current-pr --url)
echo $(gh current-pr --url) | pbcopy
```

`--open`

Open the PR in your default browser:

```bash
gh current-pr --open
```

`--help`

Show usage information:

```bash
gh current-pr --help
```

## How it works

1. Reads the current branch name.
2. Looks for an open PR via `gh pr list`, using the upstream branch name and fork owner from the branch's tracking config. Remotes are tried in order: the tracking remote, then `upstream`, `origin`, then every other remote. This finds PRs opened from a fork without matching another fork's branch of the same name.
3. Fetches title, merge status, reviews, and checks for the first match with `gh pr view`.

## Requirements

- Bash 3.2+ (macOS or Linux)
- GitHub CLI (`gh`) v2.0+, logged in with `gh auth login`
- `jq` 1.6+
- Git repository with a pull request for the current branch

Colour output is limited to terminals. Set `NO_COLOR=1` to turn it off.

## License

MIT
