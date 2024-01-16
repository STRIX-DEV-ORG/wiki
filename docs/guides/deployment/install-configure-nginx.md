---
description: Learn Nignx basic configurations
tags: [nginx, installation, configuration, linux, debian, deployment]
---

# GUI - Install and configure Nginx

## Objective

To show an efficient way to install and configure Nginx to serve an application.

## Content

### Introduction

To first install Nginx can be a headache, every single project might have specific configuration needs, maybe you want to redirect from a url to another one, maybe you have a SPA (Single-page application) or maybe you want to modify a file that has SSL applied.

### Prerequisites

You need to be logged into the server with a user that has superuser privileges and have access to the command line.

### Installing Nginx

We recommend to make sure you have the latest packages by executing 
```bash
sudo apt update
```
Make sure you are in the root folder by executing `cd ~`. Then, install Nginx with 
```bash
sudo apt install nginx
```
Verify the installation by executing
```bash
nginx -v
```

### Allow Nginx in firewall

Your server might be blocking all TCP communication by default, so we need to allow Nginx to handle this communication. You migh have already installed ufw, but if not, you need to install it by executing `sudo apt-get install ufw`.

Adjust firewall to allow http and https, in other words, allow `Nginx Full`

```bash
# Verify the applications that ufw is aware of
sudo ufw app list
# Allow http and https
sudo ufw allow 'Nginx Full'
# Apply previous changes
sudo ufw enable
# Check that OpenSSH and Nginx Full are allowed
sudo ufw status
```

### Check everything is ok

Make sure nginx is up and running by executing next commands:

```bash
# The active status shoud be active and running
sudo systemctl status nginx 

# This will show some IP addresses
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```
:::tip Test on your browser
If you copy the resulting IP address and paste it into your browser, you should see an nginx message
:::

### Creating the configuration file and enabling it

By default, Nginx will create a folder under `/etc/nginx` when installed, all configuration files will be written in the `sites-available` folder contained in the previously mentioned `nginx` folder. Every configuration file should be named after the domain name it will represent.

Move to `/etc/nginx/sites-available` and create the configuration file with:
```bash
# Move to sites-available folder
cd /etc/nginx/sites-available
# Create the configuration file, it doesn't need any file extension
touch ./[your-domain-name]
```
Create a symbolic link to enable the previous config file

```bash
sudo ln -s /etc/nginx/sites-available/[your-domain-name] /etc/nginx/sites-enabled/
```

### Understanding basic Nginx configurations

#### Directives

Nginx is conformed by directives, where you can have simple directives (ending with a semicolon `;`) and block directives (surronded by braces `{ }`). A block directive can contain simple directives and other block directives. If a block directive can have other directives inside braces, it is called a context (examples: events, http, server, and location). Directives placed in the configuration file outside of any contexts are considered to be in the main context. The events and http directives can reside in the main context, server in http, and location in server.

To have a better understanding of the previous explanation, look the next configuration:
```nginx
# Http belongs to main context (the config file is the main context)
http {
    # Server belongs to http context, as it is inside http
    server {
        # Location belongs to server context, as it is inside server
        location / {
            root /var/www;
        }
        location /images/ {
            root /data;
        }
    }
}
```

The `location` directive compares the given parameter (in this case `/`) against the current URI from the request and if there is a matching request, the URI will be added to the path specified in the root directive (in this case, to `/var/www`). If there are several matching location blocks Nginx selects the one with the longest prefix match. In the previous example, if you go to `/images/` it will match `/` and `/images/`, as `/images/` has the longest prefix match, it will be used.

#### Processing requests

Knowing the previous, we need to understand how Nginx processes the requests. Nginx first decides which server should process the request by comparing the `host` provided under the `server_name` directive, every `server` block is treated as a virtual server and if no `server_name` is provided, Nginx uses the empty name `""` as the server name, allowing this server to process requests without the `Host` header field. Then it looks to the `listen` directive that sets the `address` and `port` for IP, or the path for a UNIX-domain socket on which the server will accept requests.

With all the previous, we can expand our example, we are going to remove the http block and let only the server block.

```nginx
server {
    # Listen to port 8080
    listen 8080;
    # Catch all IPv6 addresses that listen to port 8080
    listen [::]:8080;
    # Sets the Host/s to catch the requests from, first name becomes the primary server name
    server_name example.com www.example.com;

    location / {
        root /var/www;
    }
    location /images/ {
        root /data;
    }
}
```

#### Setting a proxy server

There are several times where the intended usage for a specific location is to pass the requests to another server and retrieve the response from it. Imagine you have an aplication under `www.myapplication.com` and every request serves an HTML page, but whenever you receive some request to `www.myapplication.com/api/` you want it to send the request to your backend server that you already have configured, then you need a proxy server like this:
```nginx
server {
    listen 80;
    listen [::]80;

    server_name www.myapplication.com;

    location / {
        root /var/www;
    }
    location /api/ {
        proxy_pass www.myapplicationbackend.com:8080;
    }
}
```
If a keepalive connection is required (for constant frontend to backend communication for example) then you need to set `proxy_http_version 1.1;` directive. You can also set some headers by adding a `proxy_set_header` directive, for example `proxy_set_header Host $host;` or `proxy_set_header Connection '';`.

#### Giving specific files to serve

In the previous configuration documents we've used `location` with the `root` directive, that will try to 'build' the given request with the given root path, for example if you have:
```nginx
location /home/ {
    root /assets/images;
}
```
A request to `/home/front.png` will be resolved into `/assets/images/home/front.png`.

But you might want to specify the files to deliver if a specific location has been reached, like when you have a SPA (Single-page application) and to do so you need to use the `try_files` directive that checks the existence of files in the specified order and uses the first found file for request processing.

```nginx
server {
    listen 80;
    server_name someserver.com;
    root /var/www;

    location / {
        # This will try to find the given uri as a file name, if not found, it will render the index.html specified in the root directive of the previous context
        try_files $uri /index.html;
    }
}
```

#### Variables and further reading

As you've seen on some of the previous examples, we are using variables like `$uri` or `$host`, these variables are embeded variable names and can be used anywhere in the configuration files.

We know that these are only the basics to make Nginx configuratio and there are a lot of features and variables to check and understand from this tool, so if you ever need more in-depth of Nginx functionalities, we recommend you to go to the [official documentation](https://nginx.org/en/docs).

### Set current configurations to start working

If you read Nginx documentation you will see that they tell you to use `nginx -t` and `nginx -s reload` commands to load new configurations, but if this does not work, then:
```bash
# Test configuration files are correct
nginx -t

# Restart nginx so it takes the changes
sudo service nginx restart
# But you can also use...
sudo systemctl restart nginx

# Check nginx status by writing:
sudo systemctl status nginx
```

### Debugging

The first thing you should check is that you have nginx installed with `nginx -v`, then execute `nginx -t` to test your configuration files, if all files are correct, check that your files are under the `sites-available` folder and linked to the `sites-enabled` under the symbolic link.
You can also check the system status for nginx with `sudo systemctl status nginx`.
The final recommendation goes for the server configurations, where you can set the server logs file location:
```nginx
server {
    # Set where the logs will be placed
    access_log /var/log/nginx/nginx.acess.log;
    error_log /var/log/nginx/nginx.error.log;
}
```
:::note More tips and tricks
If you have any other tips or tricks with Nignx, please add them to this guide.
:::

## Versions

| Version | Description    | Responsibles                     | Date      |
|---------|----------------|----------------------------------|-----------|
| 1.0     | Guide creation | Emmanuel Antonio Ramirez Herrera | 03/01/2023 |