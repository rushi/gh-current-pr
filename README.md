## gh-current-pr

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

Print only the PR URL for piping to other commands:

```bash
gh current-pr --url
# https://github.com/owner/repo/pull/42
```

Use with other commands:

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

- Detects your current branch name
- Searches across all git remotes (prioritizes upstream then origin)
- Fetches PR details using `gh pr list` (supports PRs from forks)
- Displays merge status, reviews, and CI check status
- Fast single API call per invocation

## Requirements

- GitHub CLI (`gh`) v2.0+
- `jq` for JSON parsing
- `date` command (BSD or GNU)
- Git repository with a pull request for the current branch

## License

MIT
