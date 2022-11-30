# Dynamic Re-routing via Nginx

Redirecting from one domain to another while preserving certain url parameters. For example, `https://example.com/video?id=1234` to `https://youtube.com/video?id=1234`.

## Overview

- **OS:** Linux
- **Nginx:** 1.21.3

### Versions

- **Ubuntu:** 22.04 LTS

## Setup

### Installing Nginx

to install nginx on ubuntu, run the following commands

```bash
sudo apt install nginx
```

after installation, you can start nginx by running

```bash
sudo systemctl start nginx
```

### Configuring Nginx (HTTP)

To configure you can either quickly edit the nginx.conf by running

```bash
sudo vim /etc/nginx/nginx.conf
```

or you can create a new file in the conf.d folder by running

```bash
sudo vim /etc/nginx/conf.d/<your domain>.conf
```

then add the following to the file

```bash
server {
    listen 80;
    server_name <your domain>;
    location ~ ^/<old url>/(.*) {
        return 301 <new url>/$1;
    }
}
```
replace `<your domain>` with your domain name, `<old url>` with the url you want to redirect from and `<new url>` with the url you want to redirect to.

Now you can restart nginx by running

```bash
sudo systemctl restart nginx
```