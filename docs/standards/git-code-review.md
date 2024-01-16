---
description: Standards about how to review a pull request and/or merge request
tags: [github, review, code]
---

# STD - Code Review Guidelines

## Objective

This standard provides guidelines and best practices for reviewing code in a Merge Request (MR) or Pull Request (PR) in GitHub. The objective is to ensure high-quality code, adherence to coding standards, and effective collaboration within the development team.

## Content

### 1.Introduction

Code reviews play a crucial role in maintaining code quality and fostering collaboration among team members. This document outlines the things we must check and pro tips for conducting effective code reviews.

### 2. Code Review Checklist

When reviewing code in an MR or PR, consider the following aspects:

#### Code Quality:
- Code follows the established coding standards.
- Variable and function names are clear and descriptive.
- Code is modular and follows a DRY (Don't Repeat Yourself) approach.
- Code complexity is reasonable, and complex logic is well-documented.

#### Testing:
- Code changes include unit tests that cover new functionality.
- Existing unit tests are not broken by the proposed changes.
- Edge cases and error scenarios are covered by tests.
- If applicable, integration tests and end-to-end tests are included.

#### General Code Standards:
- The code is consistent with the project's overall architecture.
- Coding conventions, such as indentation and formatting, are followed.
- No commented-out code is present in the final submission.
- Error handling is implemented appropriately.
- If you think hardcoded values are required, you need to tell your team members to look for other solutions, if no solutions are found, keep hardcoded values, but add a comment to tell that might cause some inconveniences.

### 3. Pro Tips for Effective Code Reviews

Offer specific feedback that helps the developer understand the issue and suggests improvements.

#### I. Be Respectful and Positive
Maintain a positive and respectful tone in your comments, fostering a collaborative and inclusive environment, check the following:


##### I - A When to comment a line of code?
If the human error, vulnerability or a suggestion persist in only one line please create the comment there

##### I - B When to comment a file?
Usually when the entire file contains conflicts, is duplicated, must not be part of the changes or it was deleted before and the MR/PR is putting it back.

##### I - C When to comment the overall PR/MR?
Only if you have any additional comments, such as a summary of the comments you made on each file, we recommend adding a small compliment that makes the review feel more human.


#### II. Consider the Bigger Picture
Understand the context of the changes and how they fit into the overall project goals.

#### III. Address Security Concerns
Pay attention to potential security vulnerabilities and address them promptly.

#### IIII. Pair Programming
Consider occasional pair programming sessions for complex logic or critical vulnerabilities that could be improved; For example, if you notice a very high risk or a better solution, you can schedule a pair programming call to help your teammate understand why that might be a risk or why your solution may be better than his/she.

## Versions

| Version | Description       | Responsibles                     | Date       |
| ------- | ----------------- | -------------------------------- | ---------- |
| 1.0     | Standard creation | Ernesto Cabañas Albarran | 14/01/2024 |
