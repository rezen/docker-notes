# Running Containers

`docker run --name shamu -d -p 8003:8008 whale-greeting:1.0.0`

## Options
- `-d, --detach` Don't attach to tty, run in background
- `-e, --env` Provide env variable to container
- `--env-file` Provide a env file vs inline env variables
- `--name` Name your running container
- `--privileged` Allow privileged access to devices 
- `-v, --volume` Mount host volumes in container instance
- `-w, --workdir` Set working directory for process
- `-p, --publish` Map container ports to the host port
- `--rm` After container exits automatically remove it
- `-h, --hostname` Set hostname

docker exec -it b345khkasd /bin/bash

## Sharing Files
Containers are designed to be ephemeral, but with most apps, you have 
state you want to persist, be it files or database data. Additionally 
you may have content outside of the container you want it to access, but 
don't want it bundled into the container image (reasons of re-use and size reduction).
Mounting volumes allows you to achieve this goal when running containers.

```
# You can share a host directory with the '-v' flag
# so in the container you can access those files
# -v $host_path:$container_path

# Volumes default to read+write
docker run -v /host-dir:/data/container --name shamu whale-greeting

# But you can mount with readonly volume
docker run --name www-01 
    -v /home/user:/root:ro
    -v /var/www/html:/var/www/html
    nginx
```


## Cleanup

`$ docker rm $(docker ps -a -q)`