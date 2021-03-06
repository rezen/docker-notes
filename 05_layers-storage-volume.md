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
- https://boxboat.com/2017/07/25/fixuid-change-docker-container-uid-gid/
- https://www.jujens.eu/posts/en/2017/Jul/02/docker-userns-remap/
- https://stackoverflow.com/questions/23544282/what-is-the-best-way-to-manage-permissions-for-docker-shared-volumes
- https://medium.com/@delitescere/docker-file-permissions-and-line-endings-9aced07d70f8
- http://blog.ippon.tech/docker-and-permission-management/
- https://blog.csanchez.org/2017/01/31/running-docker-containers-as-non-root/
- https://www.tricksofthetrades.net/2016/03/14/docker-data-volumes/
- https://jpetazzo.github.io/2015/01/13/docker-mount-dynamic-volumes/
- https://deis.com/blog/2016/docker-storage-introduction/



## Volumes
Volumes are used to share data with the host and/or between containers. Volumes bypass the union filesystem.

- There are three types, `host`, `named`, `anonymous`
- https://docs.docker.com/glossary/?term=volume
- https://docs.docker.com/engine/admin/volumes/volumes/
- https://github.com/moby/moby/issues/19990 # Must read!
### Sharing
To share data between containers, create a named volume and mount that volume to containers.

```shell
# Create volume
docker volume create --name www_shared

# If you want to create a named volume that maps to a location on the host
docker volume create --opt type=none --opt device=/var/log --opt o=bind host_logs

# Mount volumes with share
docker run --name www-01 -v www_shared:/data/www_shared nginx
docker run --name www-02 -v www_shared:/data/www_shared nginx

```

### Plugins
- https://github.com/CWSpear/local-persist

## Copying Files
You can copy files from a running container to your local file system. This is pretty common
if you are using docker to build binaries for example.

- `docker cp $container:/var/log/error.log ./this-host`
- https://medium.com/@gchudnov/copying-data-between-docker-containers-26890935da3f
- https://github.com/gchudnov/docker-tools

## Cleanup
Remove unused volumes. Be careful, a volume may be unused at the moment but still have data
that you need to keep.

`$ docker volume prune`
