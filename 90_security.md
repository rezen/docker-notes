# Security
When thinking of using Docker/containers securely there a three components - the host, the container images & the running containers. At each level there
are steps you can take to reduce risk & take preventive measures.


## Host
If you have a Docker host, you must run the Docker Bench for security, it will perform 
a number of checks which you can treat as a checklist of configs to change.

### daemon
The Docker daemon needs to be locked down.

- https://github.com/nearform/devops/blob/master/packer/securing-docker/files/daemon.json

### auditd
You should be monitoring all files related to Docker for any sort of tampering.

```shell
auditctl -l 

# Append the rules to audit rules
vim /etc/audit/audit.rules
# -w /etc/docker -k docker_etc
# -w /etc/docker/daemon.json -k docker_json
# -w /etc/default/docker -k docker_etc_default
# -w /var/lib/docker -k docker_lib
# -w /usr/bin/docker -k docker_bin
```

## Images
- Ensure the images you are running don't have vulnerable components.

### clair
- https://github.com/arminc/clair-scanner
```shell
docker run -p 5432:5432 -d --name db arminc/clair-db:2017-09-18
docker run -p 6060:6060 --link db:postgres -d --name clair arminc/clair-local-scan:v2.0.1
./clair-scanner --ip 172.17.0.1  alpine:3.5
```

## Containers
- Make sure to limit resource utilization
- Limit what access & privileges running containers are givein
- For scanning running containers run [Vuls](https://vuls.io/) on the container host
- https://sysdig.com/opensource/falco/

## Other
### Links
- https://github.com/docker/labs/tree/master/security
- https://sysdig.com/blog/docker-security-landscape/
- https://opensource.com/business/14/7/docker-security-selinux
- http://blog.docker.com/2014/07/new-dockercon-video-docker-security-renamed-from-docker-and-selinux/
- https://blog.sqreen.io/docker-security/
- https://github.com/docker/docker-bench-security
- https://www.oreilly.com/ideas/five-security-concerns-when-using-docker
- https://www.slideshare.net/PhilEstes/docker-london-container-security
- https://www.slideshare.net/Docker/docker-security-workshop-slides
- https://codefresh.io/blog/using-docker-generate-ssl-certificates/
- http://tech.paulcz.net/2016/01/secure-docker-with-tls/
- https://github.com/jessfraz/amicontained
- https://coreos.com/os/docs/latest/coreos-hardening-guide.html
- https://dadario.com.br/courses/docker-security-fundamentals/
- https://www.nearform.com/blog/securing-docker-containers-on-aws/
- https://www.delve-labs.com/articles/docker-security-production-2/
- http://rhelblog.redhat.com/2016/10/17/secure-your-containers-with-this-one-weird-trick/


### Secrets
- https://hackernoon.com/managing-secrets-in-docker-swarm-6da766f1357d
- https://docs.docker.com/engine/swarm/secrets/
