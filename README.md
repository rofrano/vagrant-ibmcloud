# vagrant-ibmcloud

## Vagrant environment for developing on IBM Cloud

When developing with teams that have a mixture of Mac and Windows computers, it is often desirable to provide a development environment that is common to both and avoid the inevitable "works on my computer" syndrome. To this end, and in keeping with the DevOps philosophy of _"Infrastructure as Code"_, I recommend the use of **Vagrant** to auto provision a common Linux development environment for all developers to work in which more closely emulates the environment you will find on most cloud computing runtimes.

## Setup using Vagrant

You will need both Vagrant and VirtualBox. If you don't have this software the first step is down download and install it.

Download [VirtualBox](https://www.virtualbox.org/)

Download [Vagrant](https://www.vagrantup.com/)

Then all you have to do is clone this repo and invoke vagrant:

```shell
    git clone https://github.com/rofrano/vagrant-ibmcloud.git
    cd vagrant-ibmcloud
    vagrant up
    vagrant ssh
    cd /vagrant
```

You will now be inside a virtual machine that has the IBM Cloud CLI installed along with Docker, Helm, & Kubectl. The `/vagrant` folder is shared from your host computer so that any file changes you make in that folder will remain on your computer long after the virtual machine has been destroyed.

This is how I recommend all of my development teams work. Your mileage may vary. ;-)

## What's in the Vagrantfile?

I like to copy several files from my host computer into the virtual machine so that I can developer more easily with tools like `git` and `ibmcloud`. The following files will be copied to your vm if they exist:

### Copy file: .gitconfig

If you have a `~/.gitconfig` file it will be copied into the VM to that you are known by `git` as the same poerson both inside and outside of the VM

### Copy file: id_rsa

If you have a `~/.ssh/id_rsa` file it will be copied into the VM to that you can authenticate with GitHub and other hosts using your `ssh` key.

### Copy file: .vimrc

If you have a `~/.vimrc` file it will be copied into the VM to that your vim editor is confugured the same inside of the VM as it is on your host computer.

### Copy file: apiKey.json

If you have a `~/.bluemix/apiKey.json` file it will be copied into the VM to that you can login to IBM Cloud using your developer token. To set this up, when you create a platform API key in IBM Cloud, you will see a button on the UI to download the key. It will download to a file called `apiKey.json`. If you move that file into your `~/.bluemix` folder, it will be picked up by the `Vagrantfile` and added to the VM.

To use the `apiKey.json` in place of a userid and password use the following IBM Cloud command to login:

```shell
ibmcloud login --apikey @~/.bluemix/apiKey.json
```

This eliminates having to remember userids and passwords

## Docker

This `Vagrantfile` pulls down the `alpine:latest` image which is what I use as base for all of my Docker deployments. You can add any other images you would like to be pre-fetched.
