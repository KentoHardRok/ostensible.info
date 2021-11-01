+++
title = "Dockerfu"
weight = 21
+++

#docker/dockerfile

# Dockerfile setup
The dockerfile is the file used to standup/build an image to be used in docker or podman or whatever compatible container environment. There are a few steps that are necessary and some that are optional. 

```dockerfile
FROM alpine:latest
RUN apk update && \
    apk upgrade && \ 
    apk add \
        wireguard-tools \
        iptables \
        bash
ENV WG_PORT=51820
ENV NUM_CLIENTS=5
ENV PRIV_NET=10.0.0.
ENV EXT_IP=172.16.0.10
WORKDIR /etc/wireguard
COPY wg0.conf wgpeer.conf peer_setup.conf ./
COPY createwg /usr/local/bin/
RUN chmod +x /usr/local/bin/createwg && \
    mkdir client
ENTRYPOINT ["createwg"] 
CMD ["wg-quick","up","wg0"]
```

This isnt the most perfect dockerfile but it is mine and I can walk through it pretty easily. From the top we have the `FROM` command, this sets the base image. Its not a good idea to use the latest tag for the version because it could update and break things.

The next example we have is the `RUN` tag. This is a command that is run during the build process. This is important as it is not re run after the image is built so make sure this is used to establish the environment for the container. 

`ENV` and not used here is `ARG`. In this ENV is used to make environmental variables inside the new image that can be used by scripts and programs inside the container once the image is run. These ENV variables can be modified during run time. ARG is similar but only used during the image being built. These values can not be modified during runtime. 

`WORKDIR` does exactly that, changes the working directory while image is built. 

`COPY` is used to copy files to and from the container.

`ENTRYPOINT` is the next interesting command with its brother `CMD`. they are both commands that are run during image run time. so when you say `docker run <image>` these commands are run, the difference between these two is that entrpoint cannot be changed with a command line argument during runtime BUT CMD can be changed. ENTRYPOINT cannot be changed but CMD can be changed. easy enough right? [source](https://phoenixnap.com/kb/docker-cmd-vs-entrypoint)

The real beauty in all of this is when you run a command or process using a container, it can be the perfect environment for that application, guaranteed to run then bail and disappear when finished. you just have to know what that environment shoud look like.