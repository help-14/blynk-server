# Blynk Server Docker Image

Runs your own [Blynk Server](https://github.com/blynkkk/blynk-server) in a Docker container on your Raspberry Pi.

[Blynk](http://www.blynk.cc) is the "first drag-n-drop IoT app builder for Arduino, Raspberry Pi, ESP8266, SparkFun boards, and others." Super fun.

## How To Use It

### Docker compose

```
version: "3.0"
services:
  blynk:
    image: help14/blynk-server-pi
    container_name: blynk
    cap_add:
      - ALL
    volumes:
      - ./blynk:/data
    ports:
      - 8080:8080/tcp
      - 8441:8441/tcp
      - 9443:9443/tcp
      - 8080:8080/udp
      - 8441:8441/udp
      - 9443:9443/udp
    restart: unless-stopped
    #networks:
    #  myvlan:
    #    ipv4_address: 192.168.1.21
```

### Docker command

Easy peasy:

```sh
docker run help14/blynk-server-pi:latest
```

To forward IP ports from the host to the container, do this:

```sh
docker run -p 8080:8080 -p 8441:8441 -p 9443:9443 help14/blynk-server-pi:latest
```

To persist data, mount a directory into the container:

```sh
docker run -v $(PWD):/data help14/blynk-server-pi:latest
```

To include your own server.properties file, mount it into /config/server.properties

```sh
docker run -v $(PWD)/server.properties:/config/server.properties help14/blynk-server-pi:latest
```

Or you can use a data volume in another container (check out different data volume techniques [here](https://docs.docker.com/engine/tutorials/dockervolumes/)).
