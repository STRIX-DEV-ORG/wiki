# GUI - How to do correct git merge

## Objective

Show Strixdev members how to use the merge command without compromising parent branches

## Content

### Step 1 - Save your branch changes

Once the objective of your branch is finished, you should save, comment and upload the changes.

Commands:

- git add -A
- git commit -m 'Small explanation of what was done'
- git push
  
### Step 2 - Verify that the develop branch is up to date

You must go back to the develop branch and make sure that it has not undergone any updates for the moment.

Commands:

- git checkout develop
- git pull

### Step 3 - Do the merge and solve conflicts

You must go back to your branch and perform the merge to the develop branch, then you must solve each of the conflicts that can be generated when using this command.

Commands:

- git checkout your-name-branch
- git merge develop
  
### Step 4 - Creation of the pull request

To finish you must repeat the commands from step 1 again to save the union of both branches.
Later you must enter the github repository where the project is located and generate a pull request by accessing the section with the same name. This is achieved by clicking on "New pull request", selecting the develop branch as base and your branch as compare. You must write a brief explanation of your code and request a review from a team member by clicking on "Reviewers" on the right side. To finish you must click on "Create pull request"

### Step 5 - Corrections and feedback

You must make the corrections made by the other team member regarding the pull request and repeat the steps in this guide to request a review again.

## Versions

| Version | Description    | Responsibles                     | Date       |
| ------- | -------------- | -------------------------------- | ---------- |
| 1.0     | Guide creation | Erick Eduardo Avalos Riveros     | 07/07/2023 |
