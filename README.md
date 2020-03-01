# Reverse Proxy (NGINX) in Docker
This repo is the companion to [this blog post](https://coderevolve.com/reverse-proxy-in-docker/).

The default configurations here serve as a reverse proxy for the WordPress site in [this project branch](https://github.com/dawilk/coderevolve-docker-wordpress/tree/reverseproxy).

There are also some other NGINX conf examples here that can be used as a launch pad for more complex configurations.

The self-signed certificate in the ssl folder goes with the _reverseproxy-ssl.conf_ examples and the fictitious coderevolve-site.com WordPress site. **The certificate.pem and key.pem are self-signed and intended to be used as an example. You should NEVER commit valid, trusted certificate private keys to git.**

## Usage
1. Install Docker
   Linux Users: Also install docker-compose
2. Clone this repo: `git clone https://github.com/dawilk/coderevolve-docker-reverseproxy.git nginx`
3. Create the `reverseproxy` network: `docker network create reverseproxy`
4. Execute `docker-compose up -d` from the directory with the _docker-compose.yml_ file.

### Usage with other websites or applications
Modify the _./sites-enabled/coderevolve-site.conf_ template (or use one of the other examples) to suit your needs
* Replace `coderevolve-webhost` with the DNS name or IP of your web server (or container_name)
  * If the port of your web application is something other than 80, change it as well
* Replace `coderevolve-upstream` with whatever you want, just make it unique among any other upstreams
* Replace `coderevolve-site.com` with your primary web address or tld for the site

## Cleanup
If you want to remove this reverse proxy, do the following:
1. Stop and remove the reverse proxy container: `docker-compose down`
2. Remove the docker network: `docker network remove reverseproxy`
3. Remove this folder, or just clean and reset it with `git clean -fdx` and `git reset --hard`
4. [optional] Remove the nginx docker image: `docker image rm nginx`
