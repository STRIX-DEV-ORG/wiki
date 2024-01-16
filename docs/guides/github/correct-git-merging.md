---
description: Make a correct git merging
tags: [github]
---

# GUI - Correct Git merging

## Objective

Show STRIXDEV members how to use the merge command without compromising parent branches

## Content

### Save your branch changes

Once the objective of your branch is finished, you should save, comment and upload the changes.

Commands:

```git
git add -A
git commit -m 'Small explanation of what was done'
git push
```
  
### Verify that the develop branch is up to date

Follow the [git branch model standards](/standards/git-branch-model.md) by going back to the develop branch and making sure that it has not undergone any updates for the moment.

Commands:

```git
git checkout develop
git pull
```

### Do the merge and solve conflicts

You must go back to your branch and perform the merge to the develop branch, then you must solve each of the conflicts that can be generated when using this command.

Commands:

- git checkout [your-branch-name]
- git merge develop
  
### Creating the pull request

You must repeat the commands from "Save your branch changes" section to save the union of both branches.
Later you must enter the github repository where the project is located and generate a pull request by accessing the section with the same name. This is achieved by clicking on "New pull request", selecting the develop branch as base and your branch as compare. You must write a brief explanation of your code and request a review from a team member during the daily meeting or through any of the communication channles your team has agreed to use. To finish you must click on "Create pull request".

### Corrections and feedback

You must make the corrections made by the other team member regarding the pull request and repeat the steps in this guide to request a review again.

### Merging your branch

The "Reviewer" should be the one in charge of merging your pull request, if the corrections were done you must notify that and ask for a new review. If your code stays without anyone making a review for your changes for more than 7 days, you must notify your team in your daily meeting and the team must merge your branch as is.

## Versions

| Version | Description                                             | Responsibles                    | Date       |
|---------|---------------------------------------------------------|---------------------------------|------------|
| 1.0     | Guide creation                                          | Erick Eduardo Avalos Riveros    | 07/07/2023 |
| 1.1     | Fix some wording, add the "Merging your branch" section | Emmanuel Antonio Ramire Herrera | 09/01/2024 |
