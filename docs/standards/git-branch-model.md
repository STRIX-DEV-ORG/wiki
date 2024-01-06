---
description: Git branch standards
tags: [github, git-branch]
---

# STD - Git branch model

## Objective

Describe the standards to follow to work correctly with Git branches.

## Content

- STRIXDEV uses Gitflow as its branching model, which requires two main branches: "main" and "develop". The "main" branch contains the stable code that will be released to production, while the "develop" branch contains the code that is currently being worked on. In addition to the parent branches, child branches are also used to create new functionalities, fix bugs or enhance previous code.

- To name a Git branch, you need to follow the [branch naming](git-branch-naming.md) standards.

- To perform any merge into the "develop" or "main" branch, you must create a pull request and get it approved by another partner of the development team through Git.

- Before creating or merging a branch, you must verify that you are working on the most up-to-date versions of them by means of a git pull.

## Versions

| Version | Description                         | Responsibles                     | Date       |
|---------|-------------------------------------|----------------------------------|------------|
| 1.0     | Standard creation                   | Erick Eduardo Avalos Riveros     | 14/04/2023 |
| 1.1     | Fix some issues and add information | Emmanuel Antonio Ramirez Herrera | 17/04/2023 |