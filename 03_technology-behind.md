# Technology Behind

## Parts
Docker and it's related services are written primarily in `golang` which you can find
the source for on Github. Docker leverages linux kernel features to construct the isolation 
of containers

- https://github.com/docker/libnetwork
- https://github.com/opencontainers/runc
- https://www.slideshare.net/jpetazzo/anatomy-of-a-container-namespaces-cgroups-some-filesystem-magic-linuxcon
- https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/
- https://runc.io/
- https://www.opencontainers.org/
- https://ericchiang.github.io/post/containers-from-scratch/

### Docker Engine
Docker Engine does all the work, interacting with the kernel features/modules to build & run
containers. The Engine can be extended by plugins, which I'm sure is what the Enterprise Edition of 
Docker is - Docker plus awesome-sauce plugins.

### Docker API
Interactions with the engine are handled via the API. The API is a HTTP REST and you can 
interact with it using HTTP requests - so very flixble!

### Docker CLI
This is what you are typically using to interact with Docker. 

### Docker Registry
Docker images are stored in the registry, Docker Hub being the most 
common registry since it's public. You can host your own registry that 
you manage and configure Docker to use your registry.


## Kernel Features

### Namespaces
Namespaces are a linux kernel feature that allows you to isolate and virtualize a number of system resources.
With namespaces you can virtualize PIDs, hostnames, user IDs, network access, interprocess communication, & filesystems. 

- https://en.wikipedia.org/wiki/Linux_namespaces
- https://www.quora.com/How-are-Linux-namespaces-different-from-the-chroot-environment
- http://man7.org/linux/man-pages/man1/nsenter.1.html
- https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces

#### chroot
Chroot is not the same thing as namespaces but it was helpful to refer to for those familiar 
with chroots. You can thing of namespaces as a chroot++. 

- https://www.youtube.com/watch?v=HPuvDm8IC-4
- http://www.ubuntubuzz.com/2015/09/a-basic-chroot-example-in-ubuntu.html

## Control Groups 
A Linux feature that enables you to isolate, limit and audit utilization of system resources!

- https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Resource_Management_Guide/ch01.html
- https://en.wikipedia.org/wiki/Cgroups
- https://sysadmincasts.com/episodes/14-introduction-to-linux-control-groups-cgroups
- https://www.digitalocean.com/community/tutorials/how-to-limit-resources-using-cgroups-on-centos-6
- https://0xax.gitbooks.io/linux-insides/content/Cgroups/cgroups1.html

## Capabilities
Grants fine control of superuser permissions. Allows you to grant someone full power access to network
device but not kill another users process.

- https://linux-audit.com/linux-capabilities-hardening-linux-binaries-by-removing-setuid/
- https://wiki.archlinux.org/index.php/Capabilities
- http://blog.siphos.be/2013/05/overview-of-linux-capabilities-part-1/

## Fancy File System
Union File systems (allows you to patch a layer easily!)
- https://medium.com/@jessgreb01/digging-into-docker-layers-c22f948ed612
- https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/
- https://sthbrx.github.io/blog/2015/10/30/docker-just-stop-using-aufs/
- https://medium.com/@nagarwal/docker-containers-filesystem-demystified-b6ed8112a04a
- Data volume bypass default UFS
- Data volume for shared data
- Storing state

```
# View systemd config for Docker
cat $(systemctl status docker | grep loaded | grep -oP '(?<=\()([\/a-z\.]+)(?=;)')

# Find root directory
docker info | grep 'Docker Root Dir'

# Find underlying data for container
ls /var/lib/docker/containers/*/config.v2.json
```
