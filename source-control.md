## Commit Early and Commit Often

Using git for source control to improve development workflow and working in teams

* Matt Kunze - http://github.com/MattKunze

---

## Using git

* Command line
* Text editor plugins - Atom, VS Code, etc
* GUI Tools - [Sourcetree](https://www.sourcetreeapp.com/), [GitKraken](https://www.gitkraken.com/)

---

## Git Concepts - Repository

* Git project that tracks history for related files
* Tend to be one per software project, though there are arguments for monorepo

---

## Git Concepts - Remotes

* Networked copies of a repository
* Common services:
  * [GitHub](https://github.com)
  * [GitLab](https://about.gitlab.com/)
  * [Bitbucket](https://bitbucket.org/)

---

## Git Concepts - Working Copy

* Local copy of a repository
* `git clone` to create a copy of an existing repository
* `git init` to initialize a new local repository

---

## Git Concepts - Branch

* Isolate changes related to various efforts
* Lifecycle branches: `master`, `qa`, `dev`, etc
* Short-lived/feature branches: `issue-123`, `add-login-component`

---

## Git Concepts - Commit

* Set of changes, plus details about the commit (who, what, when)
* Unique _SHA_ reference - typically 7 digit number

---

## Typical Feature Workflow

* Create a branch
* Do some work
* Create a _pull request_ for review
* Merge PR to accept changes

## Feature PR - Create a branch

* `git checkout -b <branch>`
* Short and sweet for branch name
* Checkout existing branch: `git checkout <branch>`

---

## Feature PR - Commit changes

* Stage changes to commit: `git add <files>`
  * updated, new, deleted, renamed files
* Commit staged changes: `git commit`

---

## Committing Changes

Commit messages typically look like:

```
Short message describing your changes (~50 chars)

More details here, including justification for the changes, steps to reproduce
related issues, links to further information, etc
```

* Commit messages are notes to your future self
* Use links to Issues, Pull Requests, existing code, etc to tie conversations together

---

## Feature PR - Push and create PR

* `git push origin <branch>`
* Create PR online
* Reference originating issue: _Fixes #1234_

---

## Feature PR - Code Review

* Sync changes to working copy: `git fetch origin`
* Checkout branch: `git checkout <branch>`

---

## Code Review Tips

* Opportunity for a second pair of eyes to verify changes
* Be succinct, but nice

---

## Feature PR - Merge Pull Request

* Merge online - click the button
* Use cli: `git merge --no-ff <branch> && git push origin master`
* Typically delete feature branch when done

---

## Stashing Changes

* Reset changes temporarily to verify differences
* `-k` _keep_ staged changes to commit a subset of changes
* `-u` also stash _untracked_ files

---

## Reconciling Multiple Branches

* Merge - doesn't change history, produces combined output
* Rebase - move changes forward in time
* Squash - cleanup set of commits to have cleaner history

---

## Resolving Conflicts

* Occurs when merging/rebasing and the same location has changed
* Search for markers and manually resolve
* Stage/commit with merged results

---

## Random Tidbits - Aliases

* Create command line aliases for common actions
  * `gco` - `git checkout ...`
  * `ga` - `git add -A`
  * `gci` - `git commit`
  * `gnb` - `git checkout -b`
  * `gfo` - `git fetch origin`

---

## Random Tidbits - Blame

* Shows commit that introduced each line in a file
* Gitlens plugin for VSCode is awesome

---

## Random Tidbits - Bisect

* Track down when a bug was introduced
* Provide a SHA before but was introduced, and one after
* Binary search to narrow down to indivual commit

---

## Random Tidbits - Fork Model

* Typical when contributing to open source projects
* Fork you own copy of a repository
* Create feature branch and submit PR to upstream project
