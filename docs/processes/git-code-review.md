---
description: Standards about how to review a pull request and/or merge request
tags: [github, review, code]
---

# STD - Code Review Guidelines

## Objective

This standard provides guidelines and best practices for reviewing code in a Merge Request (MR) or Pull Request (PR) on GitHub. The objective is to ensure high-quality code, adherence to coding standards, and effective collaboration within the development team.

## Content

### 1.Introduction

Code reviews play a crucial role in maintaining code quality and fostering collaboration among team members. This document outlines the process and best practices for conducting effective code reviews.

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
- No hardcoded values unless if it require it.

### 3. Pro Tips for Effective Code Reviews

Offer specific feedback that helps the developer understand the issue and suggests improvements.

#### I. Be Respectful and Positive
Maintain a positive and respectful tone in your comments, fostering a collaborative and inclusive environment.

#### II. Consider the Bigger Picture
Understand the context of the changes and how they fit into the overall project goals.

#### III. Address Security Concerns
Pay attention to potential security vulnerabilities and address them promptly.

#### IIII. Pair Programming
Consider occasional pair programming sessions for complex logic or critic vulnerabilities that could be enhanced.

## Versions

| Version | Description       | Responsibles                     | Date       |
| ------- | ----------------- | -------------------------------- | ---------- |
| 1.0     | Standard creation | Ernesto Cabañas Albarran | 14/01/2024 |
