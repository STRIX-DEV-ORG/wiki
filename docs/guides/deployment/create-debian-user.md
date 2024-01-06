---
description: Create a non-root admin user for your server
tags: [linux, debian, deployment, root-user]
---

# GUI - Create Debian user

## Objective

Describe a standarized way to create Linux Debian users.

## Content

### Introduction

For several reasons it is recommended to create an admin user different to the root user, that's why we are going to show the steps required to do so, remmember that these steps are intended for Debian based Linux distrubutions.

### Prerequisites

You need to be logged into the server with your root user with superuser privileges and have access to the command line.

### Create new user

You need to choose a new username + password for the user creation, we recommend storing this information, so you don't forget about it

```bash
# Create the non-root user
adduser username
# After executing the previous command you will be asked
# for some information, rememb you will need to keep track
# of username and password, write them down...

# Give sudo privileges to the non-root user
usermod -aG sudo username
```

### Access to the new user

You have 2 options to access your newly created user:

- If you are still on your command line with your root user, you can use
```bash
sudo su username
```

- If you need to connect again to your server, now you can use your new account keys (username and password)
```bash
ssh [username]@[ip-address]
```

## Versions

| Version | Description    | Responsibles                     | Date       |
|---------|----------------|----------------------------------|------------|
| 1.0     | Guide creation | Emmanuel Antonio Ramirez Herrera | 12/12/2023 |