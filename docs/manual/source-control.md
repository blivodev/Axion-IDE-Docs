# Source Control

Axion embeds git (LibGit2Sharp) with a visual diff inspector and transactional
checkpoints.

## Everyday flow

1. Open **Source Control** (git icon). The header shows your branch and changed
   file count.
2. Stage files (or **Stage All**), review the line-by-line diff on the right.
3. Write a commit message and **Commit to main** (or your branch).
4. **Push** / **Pull** authenticate with a signed-in provider (below).

## Remote provider sign-in

The **Remote Providers & Sign-In** card connects your git host:

- Supported: **GitHub**, **Bitbucket**, **GitLab**, **gitea.com**,
  **self-hosted Gitea / custom host**.
- Sign in with username + **personal access token (PAT)**. Tokens stay local and
  are only shown masked (`••••••••abcd`).
- Push and Pull automatically use the stored credentials of the account whose
  host matches the repo's `origin`.

## Transactional checkpoints (AI safety net)

Before every AI run, Axion creates a **checkpoint stash**. If the agent's changes
are wrong, **Undo Agent Run** (top bar) rolls back to the checkpoint instantly.
Discarding checkpoints is explicit.

## Auto-save interplay

Files auto-save every 30s and after 10 edits, so the git status reflects your work
closely. Unsaved tabs show an asterisk before the next auto-save tick.
