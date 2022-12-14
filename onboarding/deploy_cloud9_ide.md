This document will help you setup a Web Based IDE for development

# Method 1: Use docker command to doploy cloud

## Install docker
```
sudo yum install docker
sudo systemctl start docker
sudo systemctl enable docker
```

## Start the dokker container
```
sudo docker run -d \
  --name=cloud9 \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Toronto \
  -p 8000:8000 \
  -v /home/centos/workspace:/code:z \
  --restart unless-stopped \
  container-registry.planetrover.ca:31320/cloud9:v0.1

```
Now you can access your ide from http://vm-ip:8000/

After start using the ide, if you need to install any package, just use apt command. e.g.

```
sudo apt update
sudo apt install vim
```

## Optional: How to build the cloud9 IDE docker image

Use following Dockerfile

```
FROM ghcr.io/linuxserver/baseimage-cloud9:latest

# Docker compose
#COPY --from=compose /usr/local/bin/docker-compose /usr/local/bin/docker-compose

RUN \
 echo "**** install docker deps ****" && \
 curl -s \
	https://download.docker.com/linux/debian/gpg | \
	apt-key add - && \
 echo 'deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable' > \
	/etc/apt/sources.list.d/docker-ce.list && \
 apt-get update && \
 apt-get install -y --no-install-recommends \
	docker-ce openssh-server net-tools && \
 echo "**** Cleanup and user perms ****" && \
 apt-get autoclean && \
 rm -rf \
	/var/lib/apt/lists/* \
	/var/tmp/* \
	/tmp/*

```

Run following command to build

```
 docker build -t container-registry.planetrover.ca:31320/cloud9:{your version here} . 
```

# Method 2: Install from scratch

# Install NVM and node.js
Make sure your system have curl installed.
```
sudo yum install curl -y 
```
Then execute the installer script as following command:
```
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash   
```
Basically, NVM keeps all files under the $HOME/.nvm directory. Then it sets environment in users .bashrc file. You need to load this environment to set required configuration by running the following command:
```
source ~/.bashrc
```

Install a specific version of nodejs
```
nvm install v10.24.1
```

# Install Cloud9

## Install requirements
```
sudo yum groupinstall -y development
sudo yum install -y git glibc-static epel-release tmux
```
## Now clone the git repo and Install the Cloud9 SDK:
```
git clone https://github.com/c9/core.git c9sdk
cd c9sdk/
scripts/install-sdk.sh
```

## Run It Forever
```
sudo yum install -y npm
sudo npm install forever -g
cd c9sdk
forever start server.js -p 8080 -w ~/workspace/ -l 0.0.0.0 --auth developer:cleverpassword
```

Now you can access your ide from http://vm-ip:8080/ with the username and password you specified.

