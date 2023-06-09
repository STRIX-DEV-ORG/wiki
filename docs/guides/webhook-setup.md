# GUI - Webhook setup by hand

## Objective

To show how to configure and run the webhook on a server for a project on github.

## Content

### Introduction

These steps are based on the Digital Ocean's documentation for configure a Webhook for your repositories by hand in a Droplet, so we are also assuming that you have all site or app ready in the server and only waiting for the webhook.

We hope that you find this guide helpful, as we are trying to centralize all de documentation into a single file.

### Step 1 - Configure the github repository

To ensure proper event notifications and their destination, it's crucial to create a webhook and a responding server. Begin by setting up the webhook, followed by configuring the server.

Start by logging into your GitHub account and selecting the repository you want to monitor. Next, click on the Settings tab located in the top menu bar and select Webhooks in the left navigation menu. Click on Add Webhook in the upper right corner and enter your account password if necessary. This will take you to a page that resembles the following:

![image]{https://assets.digitalocean.com/articles/node_webhook_sync_1604/ZLBHSjF.png}

Follow these steps to create a webhook on GitHub:

- Go to the Settings tab of the repository you want to monitor.
- Click on Webhooks in the left navigation menu.
- Click on Add Webhook located in the top right corner of the page.
- In the Payload URL field, enter http://your_server_ip:8080. This is the address and port of the Node.js server you'll create soon.
- Change the Content type to application/json to ensure that the webhook sends JSON data.
- In the Secret field, enter a secret password for this webhook. You'll use this password in your Node.js server to validate requests and ensure that they came from GitHub.
- For Which events would you like to trigger this webhook, select just the push event. We only need the push event because that is when code is updated and needs to be synced to our server.
- Select the Active checkbox to enable the webhook.
- Review the fields and click on Add webhook to create it.

The ping will fail at first, but rest assured your webhook is now configured. Now let’s get the repository cloned to the server.

### Step 2 - Creating the webhook script

To create the server, we'll need to write a Node.js script. The script will do the following:

- Launch a web server on port 8080.
- Listen for requests from the webhook.
- Verify the secret we specified when we created the webhook.
- Pull the latest version of the code from GitHub.

Once we have written the script, we can run it on our server and it will be ready to listen for webhook requests from GitHub.

:::warning User Privileges 

Make sure you have the necessary permissions/privileges to create, edit, and delete files and directories, as well as execute programs that require _sudo_ privileges.

:::

```bash
cd ~ # Navigate to your home directory
mkdir ~/NodeWebhooks # Create a new directory for your webhook script called NodeWebhooks
cd ~/NodeWebhooks # Then navigate to the new directory
nano <<customName>>Webhook.js # Create a new file called as your pleasure  inside of the NodeWebhooks directory.
```

Copy/paste the following script, but make sure to replace your_secret_key and repo with the values that correspond to your project, then save and exit.

```js title="./NodeWebhooks/exampleWebhook.js"
const secret = "your_secret_here"; // Defines a variable to hold the secret you created in Step 1 which verifies that requests come from GitHub.
const repo = "~/your_repo_path_here/"; // The full path to the repository you want to update on your local disk

const http = require('http');
const crypto = require('crypto');
const exec = require('child_process').exec;

const PM2_CMD = 'cd ~ && pm2 startOrRestart ecosystem.config.js'; // This is used after pulling from GitHub to update your project. The script first changes to the home directory and then runs the variable PM2_CMD as pm2 restart the ecosystem (in our case is strapi).

http
  .createServer(function(req, res) {
    req.on('data', function(chunk) {
      let sig =
        'sha1=' +
        crypto
          .createHmac('sha1', secret)
          .update(chunk.toString())
          .digest('hex');

      if (req.headers['x-hub-signature'] == sig) {
        exec(`cd ${repo} && git pull && ${PM2_CMD}`, (error, stdout, stderr) => {
          if (error) {
            console.error(`exec error: ${error}`);
            return;
          }
          console.log(`stdout: ${stdout}`);
          console.log(`stderr: ${stderr}`);
        });
      }
    });

    res.end();
  })
  .listen(8080);
```

- Allow the port to communicate with outside web traffic for port 8080:

```bash
sudo ufw allow 8080/tcp
sudo ufw enable
```

### Step 3 - Installing the Webhook as a Systemd Service

_systemd_ is a tool used by Ubuntu to manage tasks and services. To ensure that our webhook script starts automatically during boot, we will create a service using systemd commands. Here are the steps to create a new service file:

```bash
sudo nano /etc/systemd/system/webhook.service #  you can name it as you wish but try to add 'webhook' for avoid future confusions
```

- Include the following code in the service file to instruct systemd on how to execute the script. This specifies the location of our Node.js script and provides information about our service.

```bash title=/etc/systemd/system/webhook.service
[Unit]
Description=Github webhook
After=network.target

[Service]
Environment=NODE_PORT=8080
Type=simple
User=sammy
ExecStart=/usr/bin/nodejs /home/your_user_name/NodeWebhooks/webhook.js # don't forget to put your user!
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

- Enable the new service so it starts when the system boots:

```bash
sudo systemctl enable webhook.service
```

- Now Start the service:

```bash
sudo systemctl start webhook
```

- Ensure your service is running:

```bash
sudo systemctl status webhook
```

- You’ll see the following output indicating that the service is active:

```
Output
● webhook.service - Github webhook
   Loaded: loaded (/etc/systemd/system/webhook.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2018-08-17 19:28:41 UTC; 6s ago
 Main PID: 9912 (nodejs)
    Tasks: 6
   Memory: 7.6M
      CPU: 95ms
   CGroup: /system.slice/webhook.service
           └─9912 /usr/bin/nodejs /home/sammy/NodeWebhooks/webhook.js
```

You have successfully configured your webhook and service, and can now push new commits to your repository and see the changes reflected on your server.

## Versions

| Version | Description    | Responsibles                     | Date       |
| ------- | -------------- | -------------------------------- | ---------- |
| 1.0     | Guide creation | Ernesto Cabañas Albarran         | 28/04/2023 |
