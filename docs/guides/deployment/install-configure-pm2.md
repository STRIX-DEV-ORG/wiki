---
description: Learn PM2 basic configurations
tags: [pm2, installation, configuration, linux, debian, deployment]
---

# GUI - Install and configure PM2

## Objective

To show an efficient way to install and configure PM2 to run an application.

## Content

### Prerequisites

You need to have NodeJS and npm installed in the target system. If you have any doubt, please refer to [install NodeJS in Debian](./install-nodejs-in-debian.md).

### Installing PM2

You need to make sure you are in the root folder by executing `cd ~`. Then, install pm2 globally with `npm install pm2@latest -g`.

If the previous npm install didn't work, you can try to execute:
```sh
apt update 
apt install sudo curl 
curl -sL https://raw.githubusercontent.com/Unitech/pm2/master/packager/setup.deb.sh
sudo -E bash -
```

### Updating PM2

Make sure PM2 is already installed, you can check that by executing: `pm2 --version`.

Then, just execute `pm2 update`.

### Configuring PM2
First, we make sure we centralize configuration files under a common folder, for that, we execute:

```bash
# Navigate to your home directory
cd ~ 
# Create a new directory for your configuration files called NodeWebhooks
mkdir ~/NodeWebhooks 
# Then navigate to the new directory
cd ~/NodeWebhooks 
```

- Initialize PM2, this will create a default configuration file, you need to edit that file:
```bash
# Create default ecosystem.config.js file
pm2 init
# Modify the created file
sudo nano ecosystem.config.js
```

- Replace the file content with the next lines of code, make sure you place your own values:

```js title="ecosystem.config.js"
module.exports = {
  apps: [
    {
      name: '[app-or-service-name]',
      // Path to the working app directory, you can replace it entirely
      cwd: '/var/www/[your-domain-name]', 
      // You can use your own package manager like npm
      script: 'yarn',
      args: 'start',
      env: {
        HOST: '[your-domain-name]',
        PORT: '[your-application-port]',
        NODE_ENV: 'production',
        DATABASE_HOST: 'localhost',
        DATABASE_PORT: '5432',
        DATABASE_NAME: 'dbName',
        DATABASE_USERNAME: 'postgres',
        DATABASE_PASSWORD: 'postgres_user_password',
        DATABASE_URL: 'postgresql://[databas-username]:[database-password]@[database-host]:[database-port]/[database-name]',
      },
    },
  ],
};
```

:::tip Use your values
Remember you need to modify previous values with yours. All the env variables are just examples, if you don't need any environment variables, just delete them.
:::

### Execute your project

- Execute the project by writing `pm2 start ecosystem.config.js`

- Save your PM2 configurations for whenever server needs a reboot

```bash
# Generate the startup command
pm2 startup systemd 

# Copy and paste the command provided by the previous execution

pm2 save # save the current pm2 configuration and state
```

- Make sure you have no errors by checking the execution of `pm2 logs` command, the service should be up and running

### Multiple apps with the same configuration file

If you ever require to run multiple applications at the same time with PM2, you can do that by adding other entries to the `apps` array of the `ecosystem.config.js` file that was created under `NodeWebhooks` when you executed `pm2 init`.

### Debuging PM2

If you ever have the need to debug the PM2 process run, you should first execute `pm2 list` and this will give you the list of the different processes running with PM2 and note the id of your process.

With your process id execute `pm2 info [id]` or `pm2 describe [id]` and this will give you enough information to start your debugging, you can also check your configuration file to check if any information is wrong or also, execute `pm2 monitor [id]`.

## Versions

| Version | Description    | Responsibles                     | Date       |
| ------- | -------------- | -------------------------------- | ---------- |
| 1.0     | Guide creation | Emmanuel Antonio Ramírez Herrera | 26/12/2023 |
