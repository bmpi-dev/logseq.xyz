# Infra

## GitHub

Refer this [doc](https://github.com/bmpi-dev/deprecated-github-backend#2-create-a-github-app) to create a github app.

## AWS

### S3

Create a S3 bucket named `logseq.xyz` in aws `us-east-1` region.

### Cloudfront

Create a distribution which origin is `logseq.xyz` S3 bucket, and note the distribution domain name which is the CDN.

#### Cloudfront Public keys

Refer this [doc](https://docs.aws.amazon.com/zh_cn/AmazonCloudFront/latest/DeveloperGuide/private-content-trusted-signers.html) to create a public key which can be used to sign object url uploaded by s3 client.

## AWS Lightsail

Server Size: 1G RAM, 1 vCPU, 40 GB SSD
Region: ap-southeast-1a

### Firewall

Enable `HTTPS` in `Networking -> IPv4 Firewall`.

### Frontend environment

#### Nodejs

```bash
curl -sL https://deb.nodesource.com/setup_16.x | sudo bash - && sudo apt-get install -y nodejs
sudo npm install --global yarn
```

#### CORS

```bash
sudo npm i -g @isomorphic-git/cors-proxy
cors-proxy start -d # port 9999
```

```bash
sudo cp cors-proxy.service /etc/systemd/system/cors-proxy.service
sudo systemctl daemon-reload
sudo systemctl enable cors-proxy.service
sudo systemctl start cors-proxy.service
sudo systemctl status cors-proxy.service
```

### Backend environment

#### JDK

```bash
sudo apt-get install -y software-properties-common
wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | sudo apt-key add -
sudo add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
sudo apt-get update
sudo apt-get install -y adoptopenjdk-11-hotspot
java -version
```

#### Leiningen

```bash
sudo apt-get install -y curl
curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein > lein
sudo mv lein /usr/local/bin/lein
sudo chmod a+x /usr/local/bin/lein
lein version
```

#### Clojure Command-Line Interface

```bash
sudo apt-get install -y bash curl rlwrap
curl -O https://download.clojure.org/install/linux-install-1.10.2.774.sh
chmod +x linux-install-1.10.2.774.sh
sudo ./linux-install-1.10.2.774.sh
clj
```

### Nginx && Certbot

**After setup the backend and frontend, we can config the HTTPS!**

```
sudo cp logseq.nginx /etc/nginx/sites-enabled/
```

~~Obtaining an SSL Certificate:~~ (Use Cloudflare enable HTTPS)

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d logseq.xyz -d asset.logseq.xyz
```

~~Verifying Certbot Auto-Renewal:~~ (Use Cloudflare enable HTTPS)

```bash
sudo systemctl status certbot.timer
sudo certbot renew --dry-run #  test the renewal process
```

Reload nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## Supabase

The backend database is managed by [Supabase](https://supabase.io/).

In Supabase SQL Editor, grant the user `postgres` to SUPERUSER permission:

```
ALTER USER postgres WITH SUPERUSER;
```

## Namecheap

This [logseq.xyz](https://logseq.xyz) is registried at [Namecheap](https://www.namecheap.com/).

## Cloudflare

The [logseq.xyz](https://logseq.xyz) DNS is managed by [Cloudflare](https://www.cloudflare.com/).

Please set SSL/TLS to `Flexible` mode to enable HTTPS.

Add the following DNS records:

![](https://img.bmpi.dev/36077899-b535-1a34-0545-afd45d1e9907.png)

**!!DON'T ENABLE Auto Minify!!**

## Slack

Create two slack channel which is used to receive the notification from logseq.xyz.

- LOGSEQ_SLACK_NEW_WEBHOOK
- LOGSEQ_SLACK_EXCEPTION_WEBHOOK
