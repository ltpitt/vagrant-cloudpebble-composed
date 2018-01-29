# Cloud Pebble local installer / Vagrant machine
> This repo contains how to manually install the key components of CloudPebble as submodules into a Vagrant Linux VM. It also contains a `docker-compose` file that will assemble all of them into something that runs like a real CloudPebble instance.

## Limitations

- Pebble SSO is not available; only local accounts work.
- Websocket installs are not available because pebble SSO is not available

## Prerequisites

- Oracle VirtualBox (how to install: https://www.virtualbox.org/wiki/Downloads)
- Vagrant (how to install: https://www.vagrantup.com/intro/getting-started/install.html)


## Automatic installation using Vagrant
WARNING: patience and a cup of coffee are needed :)  

`git clone https://github.com/ltpitt/vagrant-cloudpebble-composed.git && cd vagrant-cloudpebble-composed && vagrant up`

## Manual installation

### Install Ubuntu using Vagrant
NOTE: you do not need to clone the repo if you want to install manually  

`vagrant init ubuntu/xenial64`  
`vagrant up`  
`vagrant ssh`  

IMPORTANT: remember to add RAM to the VM, I've had success with 2GB but I didn't try other values, default value WILL NOT WORK

### Remove Docker IF installed
`sudo apt-get remove docker docker-engine docker.io -y`

### Install and test Docker
`sudo apt-get update && sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && sudo apt-get update && sudo apt-get install docker-ce -y && sudo docker run hello-world`

If everything went fine you should see the Docker "Hello World" and you can proceed to the next step

### Install docker-compose
`sudo apt-get install docker-compose -y`

### Install node
`sudo apt remove nodejs npm && curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - && sudo apt-get install -y nodejs`

### Install CloudPebble
`git clone https://github.com/ltpitt/vagrant-cloudpebble-composed.git && cd vagrant-cloudpebble-composed && git clone https://github.com/ltpitt/cloudpebble.git && git clone https://github.com/ltpitt/cloudpebble-qemu-controller.git && git clone https://github.com/ltpitt/cloudpebble-ycmd-proxy.git`

### Install PebbleJs
`cd cloudpebble/ext && git clone https://github.com/pebble/pebblejs.git cloudpebble/ext && cd ../../`

### Be sure that you are in vagrant-cloudpebble-composed dir and run
`sudo chmod +x dev_setup.sh && sudo ./dev_setup.sh`

### If everything worked fine you can start CloudPebble
`sudo docker-compose up`


## A few useful Docker commands
### Stop all containers
`docker stop $(docker ps -a -q)`
### Delete all containers
`docker rm $(docker ps -a -q)`
### Delete all images
`docker rmi $(docker images -q)`


## How to use

Point your web browser to http://localhost

## Release History

* 0.0.1
    * Vagrantfile is now included, manual steps are tested.
    * A bug prevents images to be cloned from github repo

## Meta

Davide Nastri – [@pitto](https://twitter.com/pitto) – d.nastri@gmail.com

Distributed under the GPL license. See ``LICENSE`` for more information.

[https://github.com/ltpitt/vagrant-cloudpebble-composed](https://github.com/ltpitt/)

## Contributing

1. Fork it (<https://github.com/ltpitt/vagrant-cloudpebble-composed/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
