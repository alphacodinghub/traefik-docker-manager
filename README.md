# Using Traefik to manage multiple Docker applications

<a href="https://github.com/alphacodinghub/v2ray-docker/"><img src="https://img.shields.io/badge/Docker-v2ray-4BC51D.svg?style=flat"></a>
![](https://img.shields.io/badge/language-Web-orange.svg)
![](https://img.shields.io/badge/platform-Docker-lightgrey.svg)[![](https://img.shields.io/badge/Traefik-v2.x-blue.svg)](https://containo.us/traefik/)
![](https://img.shields.io/badge/license-MIT-000000.svg)

**This project aims to set up a production environment on a VPS for you to easily deploy and manage /monitor Docker applications.**

## Assumptions

- You have a VPS with Docker Engine and docker-compose and git installed.
- You have configured your domain and sub-domains to point to the IP address of the above VPS.

## Components of the Project

[**_Traefik_**](https://traefik.io) is a popular Docker-aware reverse proxy. One of its important feature is the integration with Let's Encryption functionality, which enables automatically generate and renew ssl certificates for Docker applications under its management.

In this project, we will set up a basic Docker app management environment using Traefik together with commonly used tools including Adminer and Portainer.

[**_Adminer_**](https://www.adminer.org/) (formerly known as PHPMyAdmin) is a tool for managing content in MySQL databases. It is a light-weight database managing tool. Adminer also supports SQLite, PostgreSQL, Oracle, etc. and it is distributed under GPL v2 license in the form of **a single PHP file** (around 430KB in size). Adminer development priorities are: 1. Security, 2. User experience, 3. Performance, 4. Feature set, 5. Size. [Here](https://www.adminer.org/en/phpmyadmin/) are some discussions on why Adminer is better than phpMyAdmin.

[**_Portainer_**](https://www.portainer.io/) is a lightweight open-source management UI which allows you to easily manage your different Docker environments.Portainer makes it easier for you to manage your Docker containers, it allows you to manage containers, images, networks, and volumes from the web-based Portainer dashboard.

[**_Let's Encrypt_**](https://letsencrypt.org/) enables **HTTPS** on your websites by using [ACME protocol](https://tools.ietf.org/html/rfc8555) to generate and renew SSL certificates for you.

[**_Cats Demo_**](https://hub.docker.com/r/mikesir87/cats) shows you some interesting cats gif pictures as a demo of how to deploy a Docker app.

## Features of the Project

- A production ready environment for you to easily deploy, manage and monitoring Docker apps.
- Traefik will automatically generate and renew SSL certificates for your Docker apps.
- Traefik will redirect all HTTP requests to HTTPS.
- A basic auth mechanism (witn username/passowrd) is applied to the access to Traefik and Adminer dashboards. A Traefik auth middleware template is provided in the project folder `./config/traefik/config`. You can use [htppasswd tool](https://hostingcanada.org/htpasswd-generator/) to generate your favourate username and password.
- You can access to Adminer dashboard to manage you databases.
- You can access to Portainer dashboard to monitor your Docker apps. You can also use Portainer APP Templates to deploy your new docker apps such as Wordpress, Redmine, Jenkins, Magento 2, etc.

## Customize the project settings

We use `.env` file to customize project settings. The `docker-compose` command will read the `.env` file and set the environmet variables, which will be used in `docker-compose.yml` file.

`.env_template` is provided as `.env` template. The final `.env` file will look like this:

```
APP_DOMAIN=example.com
ACME_EMAIL=alphacodinghub@example.com
```

ACME_EMAIL is your email address which is used by Let's Encrypt to generate and renew SSL certificates.

## Run the project

On your VPS, you just need to clone this project to a folder, say `/app`; create your `.env` file; run the project:

```
- mkdir /app
- cd /app
- git clone https://github.com/alphacodinghub/traefik-docker-manager.git
- cd traefik-docker-manager
- cp .env_template .env
- vim .env
- # set your APP_DOMAIN and ACMS_EMAIL, and save and quit the .env file
- docker-compose up -d
```

## Access to your dashboards

_Replace `example.com` with your own domain in the below_

- > Access to Traefik dashboard: `https://traefik.example.com`
- > Access to Aminer dashboard: `https://adminer.example.com`
- > Access to Portainer dashboard: `https://portainer.example.com`
- > Access to cats demo: `https://cats.example.com`
