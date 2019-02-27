# Prerequisites
Needed for mounting synced folders:

    vagrant plugin install vagrant-vbguest

Needed for vagrant provision docker-compose:

    vagrant plugin install vagrant-docker-compose

# vagrant up fails to mount folders
Workaround

    vagrant ssh
    sudo yum update -y
    exit
    vagrant reload

# my Ad-Hoc commands
## Install Jenkins as container
`docker run -u root --rm -d -p 8080:8080 -p 50000:50000 -v jenkins-data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkinsci/blueocean`

## Docker Quick Start Guide
~~~
alias RMAC='docker container rm --force $(docker container ls --all --quiet)'
docker container ls --all
docker image ls --all

docker container inspect -f '{{json .Config}}' web-server1 | jq '.Labels'

docker container run --detach --name web-server2 --publish 8082:80 nginx
~~~

## Mastering Docker - Third Edition
~~~
docker image build --tag local:dockerfile-example .
docker container run --detach --name dockerfile-example --publish 8080:80 local:dockerfile-example

cd env-example
docker image build --tag local/apache-php:7 .
docker container run --detach --name apache-php7 --publish 8080:80 local/apache-php:7
docker container run --detach --name apache-php5 --publish 9090:80 local/apache-php:5

cd multi-stage
docker image build --tag local:go-hello-world .
docker container run --detach --name go-hello-world --publish 8000:80 local:go-hello-world

docker container run --detach --name web-server2 --publish 8082:80 nginx
docker container exec web-server2 date
docker container top web-server2
docker container stats web-server2
# docker container inspect -f '{{json .Config}}' web-server1 | jq '.Labels'
docker container inspect web-server2 | jq
docker container inspect web-server2 | grep -i memory
docker container update --cpu-shares 512 --memory 128M --memory-swap 256M web-server2

for i in {1..5}; do docker container run -d --name nginx$(printf "$i") nginx; done
docker container stop --time 60 nginx3
docker container port nginx1

docker container run --detach --name redis --network moby-counter redis:alpine
docker container run --detach --name moby-counter --network moby-counter --publish 8080:80 russmckendrick/moby-counter

docker container stop redis
docker container rm redis
docker container run --detach --name redis -v 4a7d79781a86b4e230c44ddfec52b40643782a0efa5307c691c612a436d61b78:/data --network moby-counter redis:alpine

docker volume create redis_data
docker container stop redis
docker container rm redis
docker container run --detach --name redis -v redis_data:/data --network moby-counter redis:alpine


docker-machine create -d virtualbox swarm-manager
~~~

# References and Inspiration
* https://technology.amis.nl/2018/05/21/rapidly-spinning-up-a-vm-with-ubuntu-and-docker-on-my-windows-machine-using-vagrant-and-virtualbox/
* Disaster Girl Meme [Worked fine in dev ops problem now](http://www.developermemes.com/2013/12/13/worked-fine-dev-ops-problem-now/)
* Mastering Docker - Third Edition, By Russ McKendrick, Scott Gallagher, October 2018, [Link](https://www.packtpub.com/virtualization-and-cloud/mastering-docker-third-edition)
* Docker Quick Start Guide, By Earl Waud, November 2018, [Link](https://www.packtpub.com/networking-and-servers/docker-quick-start-guide)
