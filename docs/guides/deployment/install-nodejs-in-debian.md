---
description: How to install and globally configure NodeJS
tags: [nodejs, installation, configuration, linux, debian]
---

# GUI - Install NodeJS in Debian

## Objective

Describe a standarized way to install NodeJS uder a Debian Linux distribution environment.

## Content

### Introduction

Serveral times you are going to need to use NodeJS for your application to work, but most of the OS won't have NodeJS installed by default, so you need to make sure to install it correctly.

### Prerequisites

You need to be logged into the server with a user that has superuser privileges and have access to the command line.

### Install NodeJS

If you just want the latest release for NodeJS to be installed, just execute these commands:

```bash
sudo apt update # Grant you are using most recent packages
sudo apt install nodejs # Install the latest/stable release
sudo apt install npm # Make sure npm gets installed
node --version # Check your NodeJS version
npm --version # Check your npm version
```

### Different version from the latest

Sometimes the app development requires for a specific NodeJS version to be installed, then, you need to execute these comands:
```bash
# If you need any other node version...
sudo npm cache clean -f # Force to clean any npm cache
sudo npm install -g n # Install node helper
sudo n [version] # sudo n 18.15.0 as example
node --version # Check your node version
```

### Give execution privileges to all users

You now have NodeJS installed, but it might only work with your current user, you can give privileges to all users by executing:

```bash
cd ~ # Go to root folder
mkdir ~/.npm-global # Create node global directory
npm config set prefix '~/.npm-global' # Global node_modules will be installed here
sudo nano ~/.profile # Create or modify profile file
--------------------
# Add these lines
# set PATH so global node modules install without permission issues
export PATH=~/.npm-global/bin:$PATH
--------------------
source ~/.profile # Use previous file as system variables
```

## Versions

| Version | Description    | Responsibles                     | Date       |
|---------|----------------|----------------------------------|------------|
| 1.0     | Guide creation | Emmanuel Antonio Ramirez Herrera | 12/12/2023 |