# VERSION A: Install Docker on a Raspberry Pi

hid-sp18-503

Docker is now supported on ARM processors. Thus the instalation of
docker on Raspbery PI's is extremely simple and we do not need any
special setup to get docker running.

To install docker on the raspberry pi, please execute the following
steps:

First, ssh into the raspberry pi (or login using a monitor and open
terminal) Second, run the following command

```curl -sSL https://get.docker.com | sh```
  
If you dont want to run docker using sudo add pi to the docker user
group as recommended using

```sudo usermod -aG docker pi```

Now any docker image built for ARM can be run. Naturally it must be
small enough to fit on the PI. PLease remember it has a very small
memory.

Please report back to us if you found useful packages and tools for
the PI.

# VERSION B: Pi Docker

Docker is a tool that allows you to deploy applications inside of software 
containers. It is a method of packaging software, to include not only your 
code, but also other components such as a full file system, system tools, 
services, and libraries. This can be useful for the Raspberry Pi because it 
allows users to run applications without lot of steps, as long as the application 
is packaged inside of a Docker image. You simply install Docker and run the
container. 


## Preparing the SD card
Download the latest Raspbian Jessie Lite image from

	https://www.raspberrypi.org/downloads/raspbian/
	

Please note that Raspbian Jessie Lite image contains the only the bare minimum
amount of packages.

## Download Etcher here:

	https://etcher.io/

Now follow the instructions in Etcher to flash Raspbian image on the SD card. 
Plbefore ejecting the SD card.

## Enable SSH on the SD Card
To prevent Raspberry Pis from being hacked the RPi foundation have now disabled
SSH on the default image. So, create a text file in /boot/ called ssh - it can 
be empty file or you can type anything you want inside it.

Please note that you have renamed the ssh.txt to ssh i.e. without extension.

Now insert the SD card, networking and power etc.

## Starting Pi
Once you boot up the Raspberry Pi, Connect using SSH

		$ ssh pi@raspberrypi.local

The password is raspberry.

For security reasons, please change the default password of the user pi
using the passwd command.

Note : If you want to change the hostname of the Pi, Use an editor and change
the hostname raspberrypi in:

		* /etc/hosts
		* /etc/hostname

## Docker Installation

## Run apt-get update
Since Raspbian is Debian based, we will use apt to install Docker.
But first, we need to update.

		sudo apt-get update
				
## Install Docker
An automated script maintained by the Docker project will create a systemd
service file and copy the relevant Docker binaries into /usr/bin/.

		$ curl -sSL https://get.docker.com | sh

## Configure Docker
			
	* Set Docker to auto-start
			
		$ sudo systemctl enable docker
				
	* Reboot the Pi, or start the Docker daemon with:

		$ sudo systemctl start docker

## Enable Docker client
The Docker client can only be used by root or members of the docker group. 
Add pi or your equivalent user to the docker group using :

		$ sudo usermod -aG docker pi
				
After executing the above command, log out and reconnect with ssh.

## Test Docker
To test docker was installed successfully, run the hello-world image.

		$ docker run hello-world
				
If Docker is installed properly, you'll see a "Hello from Docker!" message.
