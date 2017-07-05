# Monitoring, Logging & Performance

- https://www.datadoghq.com/blog/monitor-docker-datadog/
- http://5pi.de/2015/01/26/monitor-docker-containers-with-prometheus/
- https://www.sysdig.org/
- https://goldmann.pl/blog/2014/09/11/resource-management-in-docker/

## General
```shell
docker ps -s
docker stats - aka top for docker!
docker logs $(docker ps | grep mysql | cut -d' ' -f1)
docker inspect $(docker ps | grep mysql | cut -d' ' -f1)
docker inspect $(docker ps | grep mysql | cut -d' ' -f1) | jq '.[].NetworkSettings.Ports'
```

## Resource Constraints
https://docs.docker.com/engine/admin/resource_constraints/

- `--memory=128m`
- `--cpus=1.5`
- `--device-read-bps=""`
- `--blkio-weight 300` Ratio is out of 500


## Auto-Restart


## Health Checks