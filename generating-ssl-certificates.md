
# Generating SSL Certificates
A tutorial on generating your own SSL certificate for your domain name using acme.sh. Credits to [alexng353/not-a-tutorial](https://github.com/alexng353/not-a-tutorial/blob/main/nginx/Generating%20SSL%20Keys.md)
## Overview
### Specifications
* **OS:** Linux
### Versions
* **Ubuntu:** 22.04 LTS
### Prerequisites
* A domain setup with [CloudFlare](https://www.cloudflare.com/)
## Steps
### Setting up acme.sh
install acme.sh by running
```bash
curl https://get.acme.sh | sh -s email=my@example.com
```
restart bash to ensure acme.sh is in your path
```bash
exec bash
```
### Generating SSL Certificates
find your cloudflare global api key, this can be found by going to your CloudFlare Profile > API Tokens or by clicking [here](https://dash.cloudflare.com/profile/api-tokens).
using the token you found above, define the following environment variables
```bash
CF_Key="your cloudflare api key"
CF_Email="your cloudflare email"
```
generate your ssl certificate (to generate a wildcard certificate, replace `www.example.com` with `*.example.com`)
```bash
acme.sh --issue --dns dns_cf -d example.com -d www.example.com
```

If you see a message similar to the following, you have successfully generated your SSL certificates.
```bash
[Tue 22 Jun 2021 11:00:00 PM UTC] Your cert is in  /root/.acme.sh/example.com/example.com.cer
[Tue 22 Jun 2021 11:00:00 PM UTC] Your cert key is in  /root/.acme.sh/example.com/example.com.key
[Tue 22 Jun 2021 11:00:00 PM UTC] The intermediate CA cert is in  /root/.acme.sh/example.com/ca.cer
[Tue 22 Jun 2021 11:00:00 PM UTC] And the full chain certs is there:  /root/.acme.sh/example.com/fullchain.cer
```
