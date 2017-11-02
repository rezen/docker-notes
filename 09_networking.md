# Networking

Ip tables magic
custom plugins
By default container networking is is not public
Internal DNS server

- https://www.youtube.com/watch?v=k3SeQPt0f0o
- https://robinwinslow.uk/2016/06/23/fix-docker-networking-dns/
- http://www.dasblinkenlichten.com/docker-networking-101/
- https://www.ibm.com/blogs/bluemix/2016/09/private-network-peering-ibm-containers/
- https://developer.ibm.com/recipes/tutorials/networking-your-docker-containers-using-docker0-bridge/
- https://mesosphere.com/blog/2017/03/23/networking-docker-containers/
- https://technologyconversations.com/2016/04/25/docker-networking-and-dns-the-good-the-bad-and-the-ugly/
- https://jvns.ca/blog/2016/12/22/container-networking/
- http://securitynik.blogspot.fr/2016/12/docker-networking-internals-how-docker_16.html
- http://neuvector.com/blog/docker-swarm-container-networking/
- https://www.slideshare.net/lbernail/deep-dive-in-docker-overlay-networks
- https://www.pluralsight.com/courses/docker-networking

```shell
# Expose port to already running container
# Get ip of container
docker inspect $(docker ps | grep openvas | cut -d' ' -f1) | grep '"IPAddress"' | tr -s ' ' | cut -d'"' -f 4 | uniq

CONTAINER_IP=172.17.0.2
CONTAINER_PORT=9390
HOST_PORT=9390

sudo iptables -t nat -A  DOCKER -p tcp --dport "${HOST_PORT}" -j DNAT --to-destination "${CONTAINER_IP}:${HOST_PORT}"
sudo iptables -t nat -L --line-numbers
sudo iptables -t nat -D  DOCKER 
```
- https://stackoverflow.com/questions/19897743/exposing-a-port-on-a-live-docker-container