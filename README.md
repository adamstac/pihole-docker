# Pi-hole Docker

Running Pi-hole with Docker is the easiest way to run Pi-hole on your LAN. This repo makes it even easier!

## Pre-requisites

You must have Docker and Docker Compose installed. I run my Pi-hole on a Mac Mini and run Docker for Mac (Intel).

## Install and setup

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

## Updating Pi-hole

```
docker-compose down
docker-compose pull
docker image prune
docker-compose up -d
```

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
