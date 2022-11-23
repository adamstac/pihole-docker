# Pi-hole Docker

Running Pi-hole with Docker is the easiest way to run Pi-hole on your LAN. This repo makes it even easier!

## Pre-requisites

You must have Docker and Docker Compose installed. I run my Pi-hole on a Mac Mini and run Docker for Mac (Intel).

## Install and run Pi-hole

Clone the repo to your machine. I like to clone to my user root `~/pihole`.

```
gh repo clone adamstac/pihole-docker pihole
```

Then do the following to get things setup.

```
cd pihole
cp .env-example .env
vim .env
```

Set your `.env` file as you'd like. Here's my example.

```
HOSTNAME="192.169.100.10 (minipro.lan)"
WEBPASSWORD="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TZ="America/Chicago"
```

Pull the Docker image and and run it.

```
docker-compose pull
docker-compose up -d
```

You should now be running Pi-hole via Docker.

You should something like this in your terminal.

```
[+] Running 2/2
 ⠿ Network pihole_default  Created               0.0s
 ⠿ Container pihole        Started               0.4s
```

You can confirm Pi-hole is running with the following command.

```
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Image}}\t{{.Status}}"
```

You should see output like this.

```
CONTAINER ID   NAMES     IMAGE                  STATUS
6fb9a1ae9175   pihole    pihole/pihole:latest   Up 2 minutes (healthy)
```

## Update Pi-hole

Pi-hole will let you know in the footer of the web UI when you're running outdated. To update, run the following commands.

Pull the latest.

```
docker-compose pull
```

Then, shutdown Pi-hole.

```
docker-compose down
```

Prune any left over images, then run Pi-hole again.

```
docker image prune
docker-compose up -d
```

Your Pi-hole should be running again.

## Disk shortage error

```
vim ./etc-pihole/pihole-FTL.conf
```

Add the following.

```
CHECK_DISK=0
```

Your `pihole-FTL.conf` should look something like this after you've added this line.

```
#; Pi-hole FTL config file
#; Comments should start with #; to avoid issues with PHP and bash reading this file
CHECK_DISK=0
LOCAL_IPV4=0.0.0.0
```
