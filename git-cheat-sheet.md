# Git Command Cheat Sheet

This sheet highlights the most commonly used Git commands with context so you can move through day-to-day workflows confidently.

## Setup & Identity
- `git config --global user.name "Name"` — set your name so commits are attributed properly.
- `git config --global user.email "email@example.com"` — associate an email with your commits.
- `git config --list` — inspect current configuration values.

## Basic Workflow
- `git status` — see staged vs unstaged changes and untracked files.
- `git add <file>` — stage a file for commit; use `.` to stage everything.
- `git commit -m "message"` — snapshot staged changes with a descriptive message.
- `git diff` — view unstaged changes; add `--staged` to compare staged content.
- `git log --oneline --graph` — inspect the history with a condensed visual.

## Branches & Collaboration
- `git branch` — list local branches; `-r` for remotes.
- `git branch <name>` — create a new branch.
- `git checkout <branch>` — switch to an existing branch (`git switch` is preferred now).
- `git checkout -b <name>` — create and switch to a new branch in one step.
- `git merge <branch>` — merge another branch into your current branch.
- `git rebase <branch>` — replay your commits on top of another branch (use carefully).

## Remotes
- `git remote -v` — list remote repositories tracked by the local repo.
- `git fetch` — download commits and refs from remotes without merging.
- `git pull` — fetch + merge (or rebase) changes from the remote branch.
- `git push` — upload local commits to the remote branch; `git push --set-upstream origin <branch>` for new branches.

## Inspection & Comparison
- `git show <commit>` — display changes introduced by a commit.
- `git blame <file>` — show who changed each line and when.
- `git clean -n` — preview removal of untracked files; `git clean -f` to delete them.
- `git stash push -m "note"` — temporarily save tracked changes; `git stash pop` reapplies them.

## Undo & Repair
- `git reset --soft HEAD~1` — undo the last commit but keep changes staged.
- `git reset --hard HEAD~1` — abandon the last commit and discard changes (use with caution).
- `git checkout -- <file>` — discard changes in the working tree for a specific file.
- `git revert <commit>` — create a new commit that undoes a previous commit without rewriting history.

## Helpful Flags
- `--stat` adds a summary of changed files and insertions/deletions to many commands (e.g., `git show --stat`).
- `--amend` lets you revise the most recent commit (`git commit --amend`).
- `--force-with-lease` is safer than `--force` when pushing (fails if remote has new commits).

> Tip: chain commands with `&&` (or scripts) to enforce ordering, and always double-check `git status` before pushing.

# Combined Reference: PowerShell vs Bash Features and GitHub Workflows & Hooks

## 1. PowerShell vs Bash Feature Comparison

| **Feature**                | **PowerShell**                                                                 | **Bash**                                   | **Workaround in Bash**                                                                 |
|----------------------------|-------------------------------------------------------------------------------|-------------------------------------------|----------------------------------------------------------------------------------------|
| **Modules**               | Yes – `Import-Module` for structured cmdlets and functions                   | No native module system                  | Use `source` to load reusable scripts or create function libraries in `.sh` files     |
| **Object Pipeline**       | Yes – Pass rich .NET objects between commands                                | No – Passes plain text                   | Use JSON or key-value text; parse with `jq` or `awk` for structured data              |
| **Cross-Platform Cmdlets**| Yes – Consistent cmdlets across OS                                           | No – Commands vary by OS                 | Use POSIX-compliant commands or wrapper scripts for portability                       |
| **Type System**           | Strong typing with .NET types                                               | Weak typing (strings everywhere)         | Validate input manually or use external tools like `bc` for numeric operations        |
| **Error Handling**        | Try/Catch/Finally blocks                                                   | Basic exit codes (`$?`, `$PIPESTATUS`)   | Implement custom error handling with `trap` and conditional checks                    |
| **Package Management**    | Built-in (`Install-Module`, `Find-Module`)                                  | No native package manager for scripts    | Use `apt`, `yum`, or `brew` for system packages; custom script repos for functions    |
| **Remote Management**     | Yes – `Invoke-Command`, `Enter-PSSession`                                   | Limited – SSH only                       | Use SSH + `scp` for remote execution; combine with Ansible for automation             |
| **Integrated Help**       | Yes – `Get-Help` for cmdlets                                                | Limited – `man` pages for commands       | Add comments and `--help` flags in custom scripts                                     |
| **Tab Completion**        | Advanced, context-aware                                                    | Basic filename completion                | Enable `bash-completion` package for improved completion                              |
| **Configuration Profiles**| Yes – `$PROFILE` for startup scripts                                        | Yes – `.bashrc`, `.profile`             | Use `.bashrc` for aliases, functions, and environment variables                       |

---

## 2. Popular GitHub Workflows (via GitHub Actions)

| **Workflow**                | **Description**                                                                 |
|-----------------------------|---------------------------------------------------------------------------------|
| **CI/CD Pipeline**          | Automates build, test, and deployment whenever code changes are pushed or PRs are opened. |
| **GitHub Flow**             | Lightweight branching workflow for frequent deployments. Uses feature branches and pull requests for collaboration. |
| **Pull Request Workflow**   | Runs tests, linters, and security checks when a PR is opened or updated. Helps maintain code quality before merging. |
| **Scheduled Jobs**          | Executes tasks at defined intervals using cron syntax (e.g., nightly builds, dependency updates). |
| **Release Workflow**        | Automates tagging, changelog generation, and publishing releases when a new version is created. |
| **Deployment Workflow**     | Deploys code to environments (e.g., staging, production) after successful builds/tests. Often integrated with cloud services. |
| **Security Scan Workflow**  | Runs vulnerability scans (e.g., CodeQL) on code changes to detect security issues early. |
| **Cache & Artifact Workflow**| Speeds up builds by caching dependencies and storing build artifacts for later use. |

---

## 3. Most Common Git Hooks

| **Hook**            | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| **pre-commit**       | Runs before a commit is finalized. Commonly used for linting, formatting, or running quick tests. |
| **prepare-commit-msg**| Modifies the default commit message before the editor opens (e.g., adding ticket IDs). |
| **commit-msg**        | Validates commit messages (e.g., enforcing conventional commit format). |
| **pre-push**          | Runs before pushing to a remote. Often used to run tests or security checks. |
| **post-merge**        | Executes after a merge. Useful for reinstalling dependencies or rebuilding assets. |
| **pre-receive (server-side)**| Blocks pushes that violate policies (e.g., pushing to `main` directly). |

