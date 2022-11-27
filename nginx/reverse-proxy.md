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

### Configuring Nginx
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