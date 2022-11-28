# Reverse Proxy via Nginx
Setting up reverse proxy via Nginx with and without SSL.
> Note: If you would like to setup reverse proxy via Nginx with SSL, please refer to [Generating SSL Certificates](../generating-ssl-certificates.md) first.

## Overview
### Specifications
* **OS:** Linux
* **Nginx:** 1.21.3

### Versions
* **Ubuntu:** 22.04 LTS

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
    server_name your.domain;

    location / {
        proxy_pass http://<your IPv4 address>:<port>;
    }
}
```
replace `your.domain` with your domain name, `<your IPv4 address>` with your server's IPv4 address and `<port>` with the port you want to use.

Now you can restart nginx by running
```bash
sudo systemctl restart nginx
```
After that you can navigate to your domain and you should see the website you are proxying.

### Configuring Nginx (HTTPS)
> Note: If you would like to setup reverse proxy via Nginx with SSL, please refer to [Generating SSL Certificates](../generating-ssl-certificates.md) first.

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
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name your.domain;

    ssl_certificate /root/.acme.sh/your.domain/fullchain.cer;
    ssl_certificate_key /root/.acme.sh/your.domain/your.domain.key;

    access_log /var/log/nginx/your.domain.access.log;
    error_log /var/log/nginx/your.domain.error.log;

    # Security
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers 'ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-
    GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SH
    A:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM
    -SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS';
    ssl_prefer_server_ciphers on;
    add_header X-XSS-Protection "1; mode=block";
    ssl_stapling on;
    ssl_stapling_verify on;
    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;

    client_max_body_size 100M;
    client_body_timeout 600s;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_pass http://<your IPv4 address>:<port>;
        proxy_redirect off;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
replace `your.domain` with your domain name, `<your IPv4 address>` with your server's IPv4 address and `<port>` with the port you want to use.

Now you can restart nginx by running
```bash
sudo systemctl restart nginx
```
After that you can navigate to your domain and you should see the website you are proxying.
> Note: If you have just generated the SSL certificates, and your website is not working as intented. After approving the SSL certificates, you might have to [wait anywhere from 15m to 24h for the SSL certificates to be fully generated](https://support.cloudflare.com/hc/en-us/articles/204144518-SSL-FAQ#:~:text=If%20Cloudflare%20is%20your%20authoritative,customer%20action%20after%20domain%20activation.).