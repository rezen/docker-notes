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


## Cleanup

`$ docker rm $(docker ps -a -q)`