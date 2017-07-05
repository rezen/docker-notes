# Installation
https://docs.docker.com/engine/installation

## Linux

#### RHEL
```shell
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
$ sudo yum -y install docker docker-registry
```

#### Ubuntu
```shell
$ sudo apt-get update
$ sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce
```

#### Arch
```shell
sudo pacman -S docker
```

#### Gentoo
Sorry, no quick & easy way to get things running. 
https://wiki.gentoo.org/wiki/Docker


#### Post Installation
```shell
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ systemctl enable docker
$ systemctl start docker
```

## Other
If you are Windows or Mac read this before you decide which version of Docker to use.
https://docs.docker.com/docker-for-mac/docker-toolbox/

## Mac
Coming soon!

## Windows
Docker for Windows uses Hyper-V for virtuailization of `dockeros`. If you are a Vagrant user, this is
problematic because Vagrant generally is combined with VirtualBox which conflicts with Hyper-V. If 
you don't use VirtualBox, then Docker for Windows is fine, otherwise you will need to install the 
Docker toolbox which fires up a VM in virtualbox.

If you are hip with windows CLI and use [Chocolately](https://chocolatey.org) you can install via the CLI  

```shell
choco install docker docker-compose
```

### Docker Toolbox - Windows
- http://scriptcrunch.com/run-commands-stopped-container/
- https://coderwall.com/p/2es5jw/docker-cheat-sheet-with-examples
- http://digitaldrummerj.me/docker-windows-mounting-directories/

```
# Adding shares on windows
cmd.exe> VBoxManage.exe sharedfolder add default --name "e/vcs" --hostpath "\\\\?\\e:\\vcs" --automount

# ssh into docker docker vm & exec ...
$ sudo mount -t vboxsf e/vcs /e/vcs/
```