---
description: How to name yor branches
tags: [github, git-branch]
---

# STD - Git branch naming

## Objective

Understand the structure needed to name a Git branch to make it easier to identify your target.

## Content

### General structure

All branches must follow the following structure: (type)/(title)
Except when the modification is related to the wiki, in which case the structure is: (type)/(artifact)-(title) 

#### Type

It indicates what the objective of the new branch is and it can be:
- f: feature, it is used when you are going to create a new feature or function
- e: enhancement, it is used when you are going to modify or improve something existing
- b: bug, it is used when you are going to repair a bug

#### Artifact

Indicates which document you are working with and can be:
- prs: process, when what is being created or modified is a process
- pol: policy, when what is being created or modified is a policy
- tmp: template, when what is being created or modified is some template
- gui: guide, when what is being created or modified is a guide
- std: standard, when what is being created or modified is some standard
- glo: glossary, when what is being created or modified is an entry in the glossary
  
#### Title

The "title" is open, but it must take into account the following standardizations:
- kebab-case: when the title consists of several words, separate the words with hyphens
- English: all titles must be written in English
- concise: the title should summarize as concisely as possible the intention of the branch

#### Examples

-Creating a template for processes

f/tmp-process

-Modification of the github-branches policy

e/pol-github-branches

-Correction of a bug in login

b/login

## Versions

| Version | Description                   | Responsibles                     | Date       |
|---------|-------------------------------|----------------------------------|------------|
| 1.0     | Create guide                  | Erick Eduardo Avalos Riveros     | 14/04/2023 |
| 1.1     | Move from guides to standards | Emmanuel Antonio Ramirez Herrera | 12/12/2023 |
