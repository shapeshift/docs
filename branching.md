# Branching

We use [git-flow](https://danielkummer.github.io/git-flow-cheatsheet/) for our branching strategy.

### General Concepts

- Develop branch always up to date with master/main branch.
- Release branches always up to date with master/main.
- Feature branches always up to date with latest develop branch.

### Branching

- Feature

  - The development branch is where all new features are merged into.
  - Features branch off of the develop branch. Feature branches always start with the prefix `feature/`

- Develop

  - The develop branch is the main branch for current development. When features are thought to be done and code reviewed, they are merged into the develop branch. Though not considered stable, this branch has the most up-to-date features in it.

- Release

  - Releases are created off of the develop branch when the develop branch is in a good state to create a release candidate. Release branches always start with the prefix `release/`
  - Release branches are release candidates that, if successfully passed through QA, will be merged into the master/main branch, then back merged into the develop branch.

- Hotfix

  - Hotfix branches happen off master/main and are merged into master and then develop. Hotfix branches always start with the prefix `hotfix/`

- Stable
  - Master/main branch current stable ready app.
  - Master/main branch only gets merges from hotfix or release branches.
