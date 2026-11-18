# Changelog

Notable changes to this project. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## Unreleased

### Fixed

- Review times on macOS showed UTC as local time. `jq` now converts `submittedAt` to local time on both BSD and GNU systems, and `date` is no longer required.
- Failing and pending commit statuses (`StatusContext`, reported by external CI services) were never listed. Only check runs were.
- A PR from another fork with the same branch name could match. The lookup now keeps only PRs whose head owner matches the tracking remote.
- A local branch tracking a differently named remote branch (`foo` tracking `origin/feature-foo`) searched for the local name. The lookup now uses the upstream branch name from git config.
- With no PR for the branch, the script exited 1 without printing "No pull request found".
- `--open` failed outside macOS. It now uses `gh pr view --web`.
- A PR title containing a backslash sequence such as `\c` was cut short.
- Colour codes were written into pipes and files. Colour is now limited to terminals and turned off by `NO_COLOR`.
- Unknown arguments were ignored. They now print the usage text and exit 1.

### Changed

- Remotes are tried in the order: tracking remote, `upstream`, `origin`, then every other remote.
