# Introduction
Docker is a container platform (open-source newly renamed moby) that helps developers
develop, test, & ship their applications in self-contained units called containers
in a fast, secure & reliable manner.  Docker was built by engineers at a PaaS company 
called dotCloud which open-sourced Docker 2013. Since then Docker has become the front-runner 
container platform, with support on a a number of vendors. Currently AWS, Azure, GoogleCompute, Heroku 
& a number  of other vendors support deploying your `Docker` configured projects!

## What is a container
The term encapsulates the fuctionality it serves ... an object that contains everything
you need to run your application. Docker explains "A container image is a lightweight, stand-alone, 
executable package of a piece of software that includes everything needed to run it: code, runtime, 
system tools, system libraries, settings."

- https://www.docker.com/what-container
- http://www.infoworld.com/article/3072929/linux/containers-101-linux-containers-and-docker-explained.html
- https://opensource.com/article/17/7/how-linux-containers-evolved

### Alternatives
https://coreos.com/rkt/docs/latest/rkt-vs-other-projects.html#rkt-vs-runc
- rkt
- containerd
- lxc

### Comparison to VM
Immediately many people draw comparisons to VMS & think of containers as mini VMs. 
A VM should contain everything you need to run your application, a VM image ~ a container image, right? 
It is correct that both VMs and containers have goals to package applications in a portable manner, but containers
have additional goals and benefits over VMs.

A VM is an entirely separate system & OS on top of your host OS. Containers on the other hand live on 
the host OS & share the kernel. There is much less isolation with and less layers separating. Because 
a container shares the same kernel and doesn't have the overhead of another OS, they are very quick
to boot!

- http://web.archive.org/web/20150326185901/http://blog.dotcloud.com/under-the-hood-linux-kernels-on-dotcloud-part
- https://blog.docker.com/2016/05/vm-or-containers/
- https://stackoverflow.com/questions/16047306/how-is-docker-different-from-a-normal-virtual-machine

## History
During the time before containers, there were a number of VM/host shaped problems. 

https://www.docker.com/use-cases
- Provisioning & deployment of VMs can be slow
- Pushing security patchs to VMs & hosts are a pain
- Resources are often under utilized
- Deployment of different apps on same host not necearily smooth, consistent and isolated
- Development environments disparate from production
- For larger orgs, developer "throwing" app over the wall to ops to make run was not easy

There were some solutions to some of the problems with configuration management systems such as Puppet, Chef & Salt
but those didn't remediate all the VM problems.

## Solves
- Package your entire application dependancies
- Creating applications which can be deployed
- Shareable environments
- Fast, consistent delivery of your applications
- Responsive deployment and scaling
- Patch images easily!
https://docs.docker.com/engine/docker-overview/#what-can-i-use-docker-for


## Drawbacks
- Eats disk space for breakfast, lunch, dinner
- Less isoloation than VMs
- Added complexity of yet another tool to learn
- Networking gets complex, look at iptables
- https://www.quora.com/What-are-some-disadvantages-of-using-Docker
- https://blog.philipphauer.de/discussing-docker-pros-and-cons/


### Terms
- https://docs.docker.com/glossary/