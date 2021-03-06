# BlackLabelOps/DockerDev

Hello fellow Docker developer! This project contains a Vagrantfile for a Docker development environment. This box is a base image for my docker examples and installs the latest docker development tools, e.g. docker-compose.

Builds the [blacklabelops/dockerdev](https://atlas.hashicorp.com/blacklabelops/boxes/dockerdev) Image on Atlas. This is a Vagrant box, never use it for production!

Features:

* Tested On: Packer, Vagrant, Virtualbox 5
* Includes: CentOS 7.1, Docker Latest, Docker-Compose , Docker-Machine , Google Cloud SDK
* Available as public Vagrant box on Atlas: [blacklabelops/dockerdev](https://atlas.hashicorp.com/blacklabelops/boxes/dockerdev)
* Atlas Virtualbox provider is build daily!
* This box can be redistributed! I use Packer to repackage it as a Vagrant box.

## Build and Use Box

Simply pull from Atlas and use the box!

~~~~
$ vagrant init blacklabelops/dockerdev
~~~~

Clone the code and build it yourself.

~~~~
$ git clone https://github.com/blacklabelops/packercentos.git
$ vagrant up
$ vagrant ssh
~~~~

## Redistribute The Box

It is always interesting to snapshot the vm and redistribute it as a Vagrant box among other developers. I have implemented some scripts around Packer in order to redistribute it under [blacklabelops/dockerdev](https://atlas.hashicorp.com/blacklabelops/boxes/dockerdev).

I want to show you how to redistribute this box. In order to make sure, that you do not leave security credentials inside the running box and in order to make this build repeatable lets start with destroying and reprovisioning the current box.

~~~~
$ vagrant destroy
$ vagrant up
~~~~

Now start the script that clones and exports the vm. The script evaluates the boxes Virtualbox Id and uses VBoxManage to clone and export the running vm.

~~~~
$ ./packer/redistribute.sh
~~~~

Afterwards I use Packer to replace the default Vagrant insecure key and repackage it as a Vagrant box.

~~~~
$ packer build packer/packer.json
~~~~

Test the box before you spread it among your friends!

~~~~
$ ./packer/testBox.sh
~~~~

Read the Atlas section on how to spread the box from the cloud!

## Atlas

This project includes scripts for uploading and managing the box on [Atlas](https://atlas.hashicorp.com/) (folder atlas/). The scripts are described in this [Tutorial](https://github.com/blacklabelops/packercentos/blob/master/tutorials/versioningWithAtlas.md).

## References

* [Box Homepage](https://atlas.hashicorp.com/blacklabelops/boxes/dockerdev)
* [Vagrant Homepage](https://www.vagrantup.com/)
* [Packer Homepage](https://www.packer.io/)
* [Virtualbox Homepage](https://www.virtualbox.org/)
* [Atlas Homepage](https://atlas.hashicorp.com/)
