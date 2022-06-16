![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/denisix/wireguard?style=flat-square)
![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/denisix/wireguard?style=flat-square)
![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/denisix/wireguard?style=flat-square)
![Docker Pulls](https://img.shields.io/docker/pulls/denisix/wireguard?style=flat-square)

# Wireguard VPN
Easy setup of Wireguard VPN server using docker engine

Do you need Wireguard VPN for your private use?
A lot of documentations provides different options to setup Wireguard VPN, this one should be easy to get it running in minutes!

Information related to Wireguard VPN you can find at official website - [https://www.wireguard.com/](https://www.wireguard.com/)

### Requirements:
- linux host with recent kernel 5.x
- wireguard module installed using
```sh
sudo apt install wireguard-tools
```
- installed [docker](https://docs.docker.com/engine/install/) engine

### Setup
* manual run
```sh
docker run --rm \
  --cap-add sys_module \
  --cap-add net_admin \
	-e PUBLIC_IP=1.2.3.4 \
	-e PORT=55555 \
	-e DNS=8.8.8.8 \
	-e SUBNET=10.88 \
	-e SUBNET_PREFIX=16 \
	-e SUBNET_IP=10.88.0.1/16 \
  -p 55555:55555/udp denisix/wireguard
```

* sample **docker-compose.yml** file in case you want to run using [docker-compose](https://docs.docker.com/compose/install/) tool:
```docker-compose.yml
version: "3"
services:

  wireguard:
    image: denisix/wireguard
    environment:
      - PUBLIC_IP=1.2.3.4
      - PORT=55555
      - DNS=8.8.8.8
			- SUBNET=10.88
			- SUBNET_PREFIX=16
			- SUBNET_IP=10.88.0.1/16
    volumes:
      - ./wireguard/:/etc/wireguard/
    ports:
      - 55555:55555/udp
    cap_add:
      - SYS_MODULE
      - NET_ADMIN
    restart: unless-stopped
```


and after startup
```sh
docker-compose up -d wireguard
```


you will find **QR code** to setup your mobile client in the docker container logs:
```sh
docker-compose logs wireguard
```

as well as simple copy-paste instructions to setup your Ubuntu desktop as wireguard VPN client :)


adding **new client** peer is easy:
```sh
docker-compose exec wireguard addclient client1
```


> p.s. please give a star if you like it :wink:
