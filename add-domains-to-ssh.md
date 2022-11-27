
# Adding domain names to SSH
A tutorial on how to add domain names to SSH.
## Overview
### Specifications
* **OS:** Linux
### Versions
* **Ubuntu:** 22.04 LTS
### Prerequisites
* A domain setup with [CloudFlare](https://www.cloudflare.com/)
## Steps
### Configuring SSH on the server
Navigate to the SSH configuration file (if you cannot find the file you can create one by running `sudo touch /root/.ssh/config`:
```bash
sudo vim /root/.ssh/config
```

Add the following to the file:
```bash
Host your.domain
    HostName <your IPv4 address>
    Port <port>
```

Replace `your.domain` with your domain name, `<your IPv4 address>` with your server's IPv4 address and `<port>` with the port you want to use (default is 22).

### Configuring CloudFlare
Navigate to the DNS tab of your domain and add a new **A** record with the following values:
* **Name:** `your.domain` (same as the domain name you used in the SSH configuration file)
* **IP Address:** `<your IPv4 address>` (same as the IPv4 address you used in the SSH configuration file)
> NOTE: Make sure you do not proxy the record! 