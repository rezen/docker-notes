# Images
Creating images in Docker is easy-breezy!
https://docs.docker.com/engine/reference/builder/

```shell
docker pull php:7.1

# Pull all tagged images
docker pull -a php

# Docker build help
docker help build
```

## Dockerfile
A Dockerfile is a manifest that contains build instructions for how your
image should be constructed. Each time you use `RUN|ADD|COPY|FROM` it creates
a slice in the file system.

When you change a line in a `Dockerfile`, that line and each following will get 
rebuilt when you build.

### Linting
Lint your `Dockerfile` to ensure you are following best practices!

- https://github.com/lukasmartinelli/hadolint/releases

```shell
curl -L -O https://github.com/lukasmartinelli/hadolint/releases/download/v1.2.1/hadolint_linux_amd64
chmod +x hadolint_linux_amd64
mv hadolint_linux_amd64 dockerlint
dockerlint Dockerfile
```

### Directives
- `FROM` - You specify a base image to create your image from such as `ubuntu:latest`
- `RUN` - Run commands within the container
- `COPY` Add local files to the container image, prefer over `ADD`
- `ADD` Add local or remote files to the container image
- `CMD` Command container runs by default
- `ENTRYPOINT` Command container runs by default that you can pass args to
- `ENV`
- `ARG`
- `WORKDIR`
- `LABEL`
- https://stackoverflow.com/questions/24958140/what-is-the-difference-between-the-copy-and-add-commands-in-a-dockerfile

### Example 1
`vim Dockerfile`

```Dockerfile
FROM php:latest
RUN apt-get  update && apt-get install -y  libcurl4-openssl-dev pkg-config libssl-dev
RUN pecl channel-update pecl.php.net && pecl install mongodb
RUN mkdir -p /var/www/html && cd /var/www/html && echo '<?php echo "Howdy, I am whaley glad you are here!";' > index.php 
WORKDIR /var/www/html
CMD ["php", "-S", "0.0.0.0:8008"]
```


```
docker build --no-cache -t whale-greeting:1.0.0 . -f Dockerfile
docker run --name shamu -d -p 8003:8008 whale-greeting:1.0.0
docker exec -it shamu /bin/bash
```

### Example 2
This example shows how to use `--build-arg`

`vim Dockerfile.node`

```Dockerfile
FROM debian:jessie
RUN apt-get update && apt-get install -y curl
ARG NODE_VERSION
RUN mkdir /app && mkdir -p /opt/node && cd /opt/node && \ 
  echo $NODE_VERSION > /opt/node/version.txt && \
  printenv && \
  curl -O https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz && \
  tar --strip-components 1 -xzf  node-v$NODE_VERSION-linux-x64.tar.gz

WORKDIR /app
ENTRYPOINT ["/opt/node/bin/node"]
```

```
docker build -t node-build-arg:6.11.0 --build-arg NODE_VERSION=6.11.0 . -f Dockerfile.node
docker build -t node-build-arg:latest --build-arg NODE_VERSION=8.1.2  --build-arg CATS=meow . -f Dockerfile.node
docker run node-build-arg:latest --version
docker run node-build-arg:6.11.0 --version
docker run -v $(pwd)/test.js:/app/test.js node-build-arg test.js
```


## Cleanup
`$ docker rmi $(docker images | grep '<none>' | tr -s ' ' | cut -d ' ' -f3)`