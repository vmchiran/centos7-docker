# Prerequisites
Needed for mounting synced folders
    vagrant plugin install vagrant-vbguest
Needed for vagrant provision docker-compose
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

# References and Inspiration
* https://technology.amis.nl/2018/05/21/rapidly-spinning-up-a-vm-with-ubuntu-and-docker-on-my-windows-machine-using-vagrant-and-virtualbox/
* Disaster Girl Meme [Worked fine in dev ops problem now](http://www.developermemes.com/2013/12/13/worked-fine-dev-ops-problem-now/)
* Mastering Docker - Third Edition, By Russ McKendrick, Scott Gallagher, October 2018, [Link](https://www.packtpub.com/virtualization-and-cloud/mastering-docker-third-edition)
* Docker Quick Start Guide, By Earl Waud, November 2018, [Link](https://www.packtpub.com/networking-and-servers/docker-quick-start-guide)
