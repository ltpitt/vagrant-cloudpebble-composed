Vagrant Cloudpebble Composed
====================

This repo contains how to (and soon an install script too) install the key components of CloudPebble as submodules into a Vagrant Linux VM. It also contains a `docker-compose` file that will assemble all of them into something that runs like a
real CloudPebble instance.

Getting Started
---------------

The current compose file assumes that the docker machine/VM is accessible at 10.0.2.15. This
is true by default, but may not be true for you.

Limitations
-----------

- Pebble SSO is not available; only local accounts work.
- Websocket installs are not available because pebble SSO is not available
- You'll have to change things manually if 10.0.2.15 isn't right.


Steps
-----------

# Install Ubuntu using Vagrant (if you need also to install Vagrant: https://www.vagrantup.com/intro/getting-started/install.html)  
`vagrant init ubuntu/xenial64`  
`vagrant up`  
`vagrant ssh`   

IMPORTANT: remember to add RAM to the VM, I've had success with 4GB but I didn't try other values. Default value WILL NOT WORK  

# Install and test Docker  
`sudo apt-get remove docker docker-engine docker.io && sudo apt-get update && sudo apt-get install apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && sudo apt-get update && sudo apt-get install docker-ce && sudo docker run hello-world`  

# Install docker-compose  
`sudo apt-get install docker-compose -y`  

# Install node  
`sudo apt remove nodejs npm && curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - && sudo apt-get install -y nodejs`  

# Install CloudPebble  
`git clone https://github.com/ltpitt/vagrant-cloudpebble-composed.git && cd vagrant-cloudpebble-composed && git clone https://github.com/ltpitt/cloudpebble.git && git clone https://github.com/ltpitt/cloudpebble-qemu-controller.git && git clone https://github.com/ltpitt/cloudpebble-ycmd-proxy.git`  

# Install PebbleJs  
`cd cloudpebble/ext && git clone https://github.com/pebble/pebblejs.git`  

Change in cloudpebble-composed\docker-compose.yml IP addess to address of your Docker install by default 172.17.0.1  
Change in cloudpebble-qemu-controller\Dockerfile ENV FIRMWARE_VERSION 3.11 replace with ENV FIRMWARE_VERSION 4.3  

# Then open a terminal and cd to cloudpebble-composed dir.  
`sudo ./dev_setup.sh`  

# If everything worked fine you can start CloudPebble  
`sudo docker-compose up`  


Useful Docker commands (for generic use and not needed in CloudPebble normal install)  

# Stop all containers  
`docker stop $(docker ps -a -q)`  

# Delete all containers  
`docker rm $(docker ps -a -q)`  

# Delete all images  
`docker rmi $(docker images -q)`  

