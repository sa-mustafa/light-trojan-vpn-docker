# light-trojan-vpn-docker

Easy docker deployment for Trojan and Trojan-Go all behind automatic TLS provided by Traefik proxy
Uses under-construction template from [tmKamal](https://github.com/tmKamal/under-construction-template).

## Requirements

Follow through these steps to have a working VPN with trojan, v2ray and xray at the same time on your VPS.

1. Buy a VPS, with a late Ubuntu LTS. LTS means long-term support edition.

2. Connect to the VPS using a SSH client such as [MobaXterm](https://mobaxterm.mobatek.net), [Putty](https://www.putty.org/), or whatever you prefer.

3. Update the Ubuntu packages

   ```shell
   # Install the latest updates
   apt-get update
   ```

4. Install docker the easy way.

   ```shell
   # Install curl
   apt-get install curl -y
   # Download Docker
   curl -fsSL get.docker.com -o get-docker.sh
   # Install Docker using the stable channel (instead of the default "edge")
   CHANNEL=stable sh get-docker.sh
   # Remove install script
   rm get-docker.sh
   ```

5. Buy a domain name or use a subdomain from free services such as [DuckDns](www.duckdns.org) or [afraid.org](https://freedns.afraid.org/). 

6. Have a (sub)domain ready, pointing to your VPS IP address. Replace my.domain.com for trojan in the docker-compose.yml file. Domain names are only configured in docker script.

### Configuring Trojan

Trojan requires two things, one is the domain name that is configured previously in docker-compose.yml in two locations (one in labels and the other in volumes section). The other is the trojan password that you choose for yourself and set it in trojan.json in "PASSWORD HERE".

## Running the Script

To run the script, set an email for Let's Encrypt in the environment variables:

```shell
export ACME_EMAIL=help@domain.com
```

and run the script as follows:

```shell
docker compose up -d
```

-d is for detached mode where the console is detached from the docker command. You can run without it to see the output from all services and debug the whole process. If the domain names are correctly pointing to your VPS, the traefik service will produce the SSL certificates automatically and the services are ready to use it. You may need to run the script multiple times initially, because the SSL files are not generated immediately and some services such as trojan depend on them to work properly.
