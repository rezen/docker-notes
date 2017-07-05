# Layers, Storage, Volume

```shell
docker pull debian:jessie
docker pull php
docker pull mysql
docker pull wordpress

docker inspect debian:jessie | jq '.[0].RootFS.Layers'
docker inspect php | jq '.[0].RootFS.Layers'

docker inspect mysql:latest | jq '.[0].RootFS.Layers | length'
dockerfileview mysql:latest | egrep 'RUN|ADD|COPY|FROM' | wc -l
```

## Layers
Layers are parts of the image

## Volumes
Volumes are used to share data with the host and/or between containers. Voluems bypass the union filesystem.

- There are three types, `host`, `named`, `anonymous`
- https://docs.docker.com/glossary/?term=volume

## Copying Files
You can copy files from a running container to your local file system. This is pretty common
if you are using docker to build binaries for example.

- `docker cp $container:/var/log/error.log ./this-host`
- https://medium.com/@gchudnov/copying-data-between-docker-containers-26890935da3f
- https://github.com/gchudnov/docker-tools

## Cleanup
Remove unused volumes

`$ docker volume prune`