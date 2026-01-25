# Git Command Cheat Sheet

This sheet highlights the most commonly used Git commands with context so you can move through day-to-day workflows confidently.

## Setup & Identity
- `git config --global user.name "Name"` - set your name so commits are attributed properly.
- `git config --global user.email "email@example.com"` - associate an email with your commits.
- `git config --list` - inspect current configuration values.
- `git init` - initialize a new Git repository.


## Basic Workflow
- `git status` - see staged vs unstaged changes and untracked files.
- `git add <file>` - stage a file for commit.
- `git add .` - stage all changes (new, modified, deleted).
- `git commit -m "message"` - snapshot staged changes with a descriptive message.
- `git diff` - view unstaged changes; add `--staged` to compare staged content.
- `git log --oneline --graph` - inspect the history with a condensed visual.

## Branches & Collaboration
- `git branch` - list local branches; `-r` for remotes, `-a` for all.
- `git branch <name>` - create a new branch.
- `git branch -M main` - rename the current branch to `main`.
- `git switch <branch>` - switch to an existing branch (`git checkout <branch>` is outdated now).
- `git switch -c <name>` - create and switch to a new branch in one step. `git checkout -b <name>` also works but outdated.
- `git remote add origin https://github.com/BRudow317/<repo name>.git` - add a remote repository.
- `git push -u origin main` - push the current branch to the remote repository and set the upstream.


- `git merge <branch>` - merge another branch into your current branch.
- `git rebase <branch>` - replay your commits on top of another branch (use carefully).

## Remotes
- `git remote -v` - list remote repositories tracked by the local repo.
- `git fetch` - download commits and refs from remotes without merging.
- `git pull` - fetch + merge (or rebase) changes from the remote branch.
- `git push` - upload local commits to the remote branch; `git push --set-upstream origin <branch>` for new branches.

## Inspection & Comparison
- `git show <commit>` - display changes introduced by a commit.
- `git blame <file>` - show who changed each line and when.
- `git clean -n` - preview removal of untracked files; `git clean -f` to delete them.
- `git stash push -m "note"` - temporarily save tracked changes; `git stash pop` reapplies them.

## Delete & Cleanup
- `git branch -d <branch>` - delete a local branch (use `-D` to force).
- `git remote remove <name>` - delete a remote reference. 
- `git gc` - clean up unnecessary files and optimize the local repository.

## Undo & Repair
- `git reset --soft HEAD~1` - undo the last commit but keep changes staged.
- `git reset --hard HEAD~1` - abandon the last commit and discard changes (use with caution).
- `git checkout -- <file>` - discard changes in the working tree for a specific file.
- `git revert <commit>` - create a new commit that undoes a previous commit without rewriting history.

## Helpful Flags
- `--stat` adds a summary of changed files and insertions/deletions to many commands (e.g., `git show --stat`).
- `--amend` lets you revise the most recent commit (`git commit --amend`).
- `--force-with-lease` is safer than `--force` when pushing (fails if remote has new commits).

> Tip: chain commands with `&&` (or scripts) to enforce ordering, and always double-check `git status` before pushing.


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

```text
Install
GitHub Desktop
desktop.github.com

Git for All Platforms
git-scm.com

Configure tooling
Configure user information for all local repositories

$ git config --global user.name "[name]"

Sets the name you want attached to your commit transactions

$ git config --global user.email "[email address]"

Sets the email you want attached to your commit transactions

$ git config --global color.ui auto

Enables helpful colorization of command line output

Branches
Branches are an important part of working with Git. Any commits you make will be made on the branch you’re currently “checked out” to. Use git status to see which branch that is.

$ git branch [branch-name]

Creates a new branch

$ git switch -c [branch-name]

Switches to the specified branch and updates the working directory

$ git merge [branch]

Combines the specified branch’s history into the current branch. This is usually done in pull requests, but is an important Git operation.

$ git branch -d [branch-name]

Deletes the specified branch

Create repositories
A new repository can either be created locally, or an existing repository can be cloned. When a repository was initialized locally, you have to push it to GitHub afterwards.

$ git init

The git init command turns an existing directory into a new Git repository inside the folder you are running this command. After using the git init command, link the local repository to an empty GitHub repository using the following command:

$ git remote add origin [url]

Specifies the remote repository for your local repository. The url points to a repository on GitHub.

$ git clone [url]

Clone (download) a repository that already exists on GitHub, including all of the files, branches, and commits

The .gitignore file
Sometimes it may be a good idea to exclude files from being tracked with Git. This is typically done in a special file named .gitignore. You can find helpful templates for .gitignore files at github.com/github/gitignore.

Synchronize changes
Synchronize your local repository with the remote repository on GitHub.com

$ git fetch

Downloads all history from the remote tracking branches

$ git merge

Combines remote tracking branches into current local branch

$ git push

Uploads all local branch commits to GitHub

$ git pull

Updates your current local working branch with all new commits from the corresponding remote branch on GitHub. git pull is a combination of git fetch and git merge

Make changes
Browse and inspect the evolution of project files

$ git log

Lists version history for the current branch

$ git log --follow [file]

Lists version history for a file, beyond renames (works only for a single file)

$ git diff [first-branch]...[second-branch]

Shows content differences between two branches

$ git show [commit]

Outputs metadata and content changes of the specified commit

$ git add [file]

Snapshots the file in preparation for versioning

$ git commit -m "[descriptive message]"

Records file snapshots permanently in version history

Redo commits
Erase mistakes and craft replacement history

$ git reset [commit]

Undoes all commits after [commit], preserving changes locally

$ git reset --hard [commit]

Discards all history and changes back to the specified commit

CAUTION! Changing history can have nasty side effects. If you need to change commits that exist on GitHub (the remote), proceed with caution. If you need help, reach out at github.community or contact support.

Glossary
git: an open source, distributed version-control system
GitHub: a platform for hosting and collaborating on Git repositories
commit: a Git object, a snapshot of your entire repository compressed into a SHA
branch: a lightweight movable pointer to a commit
clone: a local version of a repository, including all commits and branches
remote: a common repository on GitHub that all team members use to exchange their changes
fork: a copy of a repository on GitHub owned by a different user
pull request: a place to compare and discuss the differences introduced on a branch with reviews, comments, integrated tests, and more
HEAD: representing your current working directory, the HEAD pointer can be moved to different branches, tags, or commits when using git switch
```