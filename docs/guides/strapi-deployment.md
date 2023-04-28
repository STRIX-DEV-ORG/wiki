# GUI - Strapi deployment by hand

## Objective

To show an efficient way for a Strapi project deployment by hand.

## Content

### Introduction

These steps are based on the Strapi's and Digital Ocean's documentation for deploying a Strapi project by hand in a Droplet, so we are also assuming that you have installed an Ubuntu Linux server that is in its 18.04 version at least. It is also important to mention that for the last modification of this file, we are using Strapi v4.

We hope that you find this guide helpful, as we are trying to centralize all de documentation into a single file, and we are also providing some other findings that have helped to solve several issues for Strapi applications deployments by hand.

### Configure the basics in your droplet, hosting, ec2, whatever tool you're using

:::tip Windows OS
If you are using a Windows Operative system, we recommend you to install OpenSSH services to use from PowerShell
:::

- Go to your service provider panel, create an ssh access door and access it from your computer by using `ssh [username]@[ip-address]` and your password/ssh key
- Don't forget to create a non-root user, for that just execute the next few bash lines

```bash
adduser username # Create the non-root user
# After executing the previous command you will be asked
# for some information, rememb you will need to keep track
# of username and password, write them down...

usermod -aG sudo username # Give sudo privileges to the non-root user
```

- Login with your new non-root user

- Add some protection rules with basic firewall configuration

```bash
sudo ufw allow OpenSSH # Allow SSH secure communication
sudo ufw enable # Make the previous rule take effect
sudo ufw status # Make sure OpenSSH is listed and Allowed
```

- Install nodejs and make sure it has execution privileges for all your users

```bash
sudo apt update # Grant you are using most recent packages
sudo apt install nodejs # Install the latest/stable release
sudo apt install npm # Make sure npm gets installed

# If you need any other node version...
sudo npm cache clean -f # Force to clean any npm cache
sudo npm install -g n # Install node helper
sudo n [version] # sudo n 18.15.0 as example
node --version # Check your node version

cd ~ # Go to root folder
mkdir ~/.npm-global # Create node global directory
npm config set prefix '~/.npm-global' # Global node_modules will be installed here
sudo nano ~/.profile # Create profile file
--------------------
# Add these lines
# set PATH so global node modules install without permission issues
export PATH=~/.npm-global/bin:$PATH
--------------------
source ~/.profile # Use previous file as system variables
```

- Make sure you have git installed, otherwise, install it by using `sudo apt install git`

### Database creation

:::tip DBMS
As several users recommend using PosgreSQL, we are going to stick to that configuration, if you ever need to use any other Database Management System, we encorage you to find the right documentation, test it and add your learnings to this document
:::

We are going to install PostgreSQL, modify the default user's password and create a database, don't forget to keep the database port, database name, user name and user's password

```bash
sudo apt update # Grant you are using most recent packages
sudo apt install postgresql postgresql-contrib # Install postgresql packages

sudo systemctl start postgresql.service # Start postgresql service

sudo -i -u postgres # Log into postgres user (it was created along postgres installation)

psql # Execute postgresql

# Change postgres user password
postgres=# ALTER USER postgres PASSWORD 'new password';

# Create the database
postgres=# createdb dbName
```

### Local/server repo configurations

:::warning Misconfigurations

Make sure you read everything here carefully, as some misconfigurations may result in several hours spent.

:::

- Create the next folder structure inside the `config` folder: `config/env/production`

- Inside `production` create a file named `database.js`, copy and paste the next snippet:

```js title="./config/env/production/database.js"
const { parse } = require('pg-connection-string');

module.exports = ({ env }) => {
  const { host, port, database, user, password } = parse(env('DATABASE_URL'));

  return {
    connection: {
      client: 'postgres',
      connection: {
        host,
        port,
        database,
        user,
        password,
        ssl: { rejectUnauthorized: false },
      },
      debug: false,
    },
  };
};
```

- Make sure you commit and push your changes to the repo

- Make sure you are loged into your server with the non-root user, navigate to `/var/www` and clone your repo by giving it `your domain name` as the name of the folder

```bash
cd /var/www # Move to folder
git clone repo-url yourdomainname # clone your repository
```

:::tip Use your domain
It is very important you clone your repo with your domain name as the name of the folder, as it will help you a lot for the following configurations
:::

- Move to your repo folder, install node dependencies and install node's posgresql dependencies too.

```bash
cd yourdomainname # Move to folder
npm install # Install project dependencies
npm install pg --save # Install posgresql dependencies
```

- Create `.env` file and add the required variables

```bash
sudo nano .env # Create and open .env file

# Make sure your file has the next variables
------------
DATABASE_PORT=value
DATABASE_NAME=value
DATABASE_USERNAME=value
DATABASE_PASSWORD=value
HOST=value
PORT=value
APP_KEYS=value
API_TOKEN_SALT=value
ADMIN_JWT_SECRET=value
JWT_SECRET=value
DATABASE_URL=value
------------

# This file will only be used for the "npm run build" command
```

- Build the project with `sudo NODE_ENV=production node run build`

### Configuring pm2, this bastard...

- Make sure you are in the root folder with `cd ~`

- Install pm2 globally with `npm install pm2@latest -g`

- Make the required configurations by executing the next command lines:

```bash
pm2 init # Create default ecosystem.config.js file
sudo nano ecosystem.config.js # Modify the created file
```

- Replace the file content with the next

```js title="ecosystem.config.js"
module.exports = {
  apps: [
    {
      name: 'app_or_service_name',
      cwd: '/var/www/yourdomainname',
      script: 'npm',
      args: 'start',
      env: {
        HOST: 'yourdomainname',
        PORT: '1337',
        NODE_ENV: 'production',
        DATABASE_HOST: 'localhost', // database endpoint
        DATABASE_PORT: '5432',
        DATABASE_NAME: 'dbName', // DB name
        DATABASE_USERNAME: 'postgres', // your username for psql
        DATABASE_PASSWORD: 'postgres_user_password', // your password for psql
        DATABASE_URL: 'postgresql://username:password@host:port/dbName',
      },
    },
  ],
};
```

:::tip Use your values

Remember you need to modify previous values with yours.
DATABASE_URL might be the only database related variable being used but provide the other database related variables as a backup

:::

- Execute the project by writing `pm2 start ecosystem.config.js`

- Save your pm2 configurations for whenever server needs a reboot

```bash
pm2 startup systemd # Generate the startup command
# Copy and paste the command provided by the previous execution

pm2 save # save the current pm2 configuration and state
```

- Make sure you have no errors by checking the execution of `pm2 logs` command, the service should be up and running

### Final, hard steps

- Install nginx

```bash
sudo apt update # Grant most recent packages are being used
sudo apt install nginx
```

- Adjust firewall to allow http and https, in other words, allow `Nginx Full`

```bash
sudo ufw allow 'Nginx Full' # Allow http and https
sudo ufw enable # Apply previous changes
sudo ufw status # Check that OpenSSH and Nginx Full are allowed
```

- Make sure nginx is up and running by executing:

```bash
sudo systemctl status nginx # The active status shoud be active and running

# This will show some IP addresses
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'

# Copy and paste the IP addresses into your browser, you should see an nginx message
```

- Make sure your folder under `/var/www` path has the right permissions

```bash
sudho chown -R $USER:$USER /var/www/yourdomainname # Assign ownership to current user
sudo chmod -R 755 /var/www/yourdomainname # Change folder permissions
```

- Create the configuration file for nginx under `/etc/nginx/sites-available`

```bash
sudo nano /etc/nginx/sites-available/yourdomainname # Create and open the file
```

- Paste the next template, we will modify this one later

```nginx title="/etc/nginx/sites-available/yourdomainname"
server {
  listen 80;
  listen [::]:80;

  root /var/www/yourdomainname;
  index index.html index.htm index.nginx-debian.html;

  server_name yourdomainname;

  location / {
    try_files $uri $uri/ =404;
  }
}
```

- Create a symbolic link to enable the previous config file

```bash
sudo ln -s /etc/nginx/sites-available/yourdomainname /etc/nginx/sites-enabled/
```

- Check that all the configurations are ok with `sudo nginx -t` and restart the nginx service with `sudo systemctl restart nginx`

- Install certbot to add SSL and create the certification

```bash
sudo apt install certbot python3-certbot-nginx # Install certbot and nginx plugin for certbot

sudo certbot -d yourdomainname # Create the certification

sudo certbot renew --dry-run # Make sure the renewal is set
```

- Modify once more the nginx config file by using `sudo nano /etc/nginx/sites-available/yourdomainname`. In the firrst 'server' entry you see, you will find some certbot related configs right under 'server_name' line and above 'listen [::]443 ssl...'. Paste the next code right between those lines and make sure everything else remains the same.

```nginx title="/etc/nginx/sites-available/yourdomainname"
 location / {
    proxy_pass http://yourdomainname:1337;
    proxy_http_version 1.1;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Server $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header Host $http_host;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "Upgrade";
    proxy_pass_request_headers on;
}
```

:::tip Rename values
Make sure that every 'server_name' and '$host' mention has your domain name as a value and that the root remains being '/var/www/yourdomainname'
:::

- Check that all the configurations are ok with `sudo nginx -t` and restart the nginx service with `sudo systemctl restart nginx`

### Furthermore

If you have followed all the previous steps and you still have some errors, please try to do it once again from the beginning, if you still have troubles, contact a teammate, and if both of you can't find a way to solve it, then you need to report this to the team.

## Versions

| Version | Description    | Responsibles                     | Date       |
| ------- | -------------- | -------------------------------- | ---------- |
| 1.0     | Guide creation | Emmanuel Antonio Ramírez Herrera | 26/04/2023 |
