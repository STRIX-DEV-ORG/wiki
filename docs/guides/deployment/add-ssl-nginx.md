---
description: Add SSL with Certbot to Nginx server
tags: [linux, debian, deployment, nginx, configuration, ssl, certbot]
---

# GUI - Add SSL to Nginx server

## Objective

To show a standarized way to install and configure an SSL certificate with autorenewal to Nginx servers by using Certbot.

## Content

### Introduction

### Prerequisites

You need to be logged into the server with your root user with superuser privileges and have access to the command line. You also need to already have an Nginx configuration up and running and python3 installed in your hosting service.

### Install dependencies

We are going to install certbot and a Python3 helper that will help us to install SSL certificates over Nginx.
```bash
sudo apt install certbot python3-certbot-nginx 
```

### Add certificate

There are two ways to add a certificate, the first one is to execute a commmand that will trigger some questions that we need to answer with:
```bash
sudo certbot -d [your-domain-name] -d [your-other-domain-or-subdomain]
```

The other one is giving the answer to this questions through flags.
```bash
sudo certbot --nginx --redirect --agree-tos --no-eff-email -m youremail@mail.com -d domain.com -d www.domain.com
```

### Enable autorenewal

The certificate has a limited ammount of time of availability, so, if you don't want to be manually generating new SSL certificates, you need to activate the autorenewal with:
```bash
sudo certbot renew --dry-run
```

### Check SSL installation

The previous commands will make modifications under your Nginx config files, so if you want to check that SSL has been successfully configurated, you can go to `/etc/nginx/sites-available/[your-domain-name]` and check its contents.

## Versions

| Version | Description    | Responsibles                     | Date      |
|---------|----------------|----------------------------------|-----------|
| 1.0     | Guide creation | Emmanuel Antonio Ramirez Herrera | 04/01/2023 |