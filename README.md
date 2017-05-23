# Deploy Ubuntu 14.04 and Varnish with Docker

### Setup the IP for the docker container
This will be the IP address which will serve the back-end "varnished".

    sudo  ifconfig en1 alias 192.168.1.200/24 up

### Varnish environment variables
Varnish will make of the following environment variables.

	VARNISH_BACKEND_PORT 80
	VARNISH_BACKEND_IP 192.168.1.213
	VARNISH_BACKEND_IP_1 192.168.1.2
	VARNISH_PORT 80

### Pre-Built image
You can use the pre-built image. After the docker pull, there is no need to run the command again, the image will be on your machine.

	$ sudo docker pull miltiadisalexis/ubuntu-varnish


### Build Image
You can easily build the image. 

	$ cd ubuntu-varnish
	$ sudo docker build miltiadisalexis/ubuntu-varnish .


### How to run the container
The container will be an ubuntu image with the varnish application.

	$ sudo docker run -i -t -p 192.168.1.200:80:80 -e VARNISH_BACKEND_IP=192.168.1.215 -e VARNISH_BACKEND_IP_1=192.168.1.211 miltiadisalexis/ubuntu-varnish /start.sh


#### Access the bash
If you want to enter in the container with root permissions.

	$ sudo docker run -i -t -p 192.168.1.200:80:80 -e VARNISH_BACKEND_IP=192.168.1.215 -e VARNISH_BACKEND_IP_1=192.168.1.211 miltiadisalexis/ubuntu-varnish bash


### Stop the container
If only one instance of this container is running this command will stop it:

	$ sudo docker stop `sudo docker ps |grep miltiadisalexis/ubuntu-varnish |cut -d\  -f1`

