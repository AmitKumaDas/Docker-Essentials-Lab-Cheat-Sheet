## Docker-Essentials-Lab-Cheat-Sheet
![image](https://github.com/AmitKumaDas/Docker-Essentials-Lab-Cheat-Sheet/assets/152639378/3fdd3e46-d2a8-4b4f-91d5-6b688799504e)
# Docker Essentials Lab Cheat Sheet

### Docker Labs Pre-requisites
1. Basic understanding of Linux Commands.
2. Basic knowledge of a Cloud platform such as AWS.
3. Good to have an AWS-Free Tier Account for Practice.
4. Copy and paste a few details of your Allocated Region to a text file that we frequently use in labs as mentioned below:
     - Region (**EX:** us-east-1)
     - Availability Zones (**EX:** us-east-1a, us-east-1b)
     - AMI IDs (**EX:** Amazon Linux, RedHat, Ubuntu)
     - VPC ID, Subnet ID, Security group ID, KeyPair Name.

## Table Of Contents
* [Lab-1: Creating an EC2 Instance in AWS and Installing Docker]
* [Lab-2: Basic Docker Commands]
* [Lab-3: Docker container life cycle]
* [Lab-4: Bind Mount in Docker](
* [Lab-5: Volume Mount in Docker]
* [lab-6: tmpfs Mount in Docker]
* [Lab-7: Docker Networking]
* [Lab-8: Dockerfile]
* [Lab-9: Pushing the image to DockerHub]
* [Lab-10: Building Efficient Docker Images]



## Lab-1: Creating an EC2 Instance in AWS and Installing Docker

To begin, log in to AWS Console.

### Task-1:  Launching EC2 instances and Connecting to EC2 Instances using SSH

* Manually Launch a `t2.micro` instance with OS version as `Ubuntu 22.04 LTS` in North Virginia (us-east-1) Region.
* Enable `SSH`, `HTTP`, `HTTPS` and `edit`.
* Type : `Custom TCP`     Source Type: `Anywhere`    Port Range : `8080-8090`
* Configure Storage: `10 GiB`
* Once Launched, Connect to the Instance using `MobaXterm` or `Putty` or `EC2 Instance Connect` with username "`ubuntu`".

### Task-2: Installing Docker on Ubuntu 18.04 operating system 
```
sudo hostnamectl set-hostname docker
```
```
bash
``` 
```
sudo su
```
```
apt update -y
```
```
apt install curl -y
```
```
curl -SSL https://get.docker.com/ | sh
```
```
service docker status   # Or systemctl status docker
```
If the service is not active, then we need to start the service
```
service docker start    # Or systemctl start docker
```
To add ubuntu user to docker group, if you are not working as the root user
```
sudo usermod -aG docker ubuntu
```
```
docker --version
```
---------------------------------**End Of Lab 1**---------------------------------
## Lab-2: Basic Docker Commands

### Task 1: Creating your first Docker container
Pull the image from Docker Hub to the Local repo and start the container
```
docker container run hello-world  
```
### Task 2: Basic Commands to run the Container in Interactive mode
Download the image from Docker Hub to the Local repo
```
docker image pull ubuntu
```
List all the images in the local repo
```
docker image ls
```
List all running processes related to containers
```
docker ps
```
List all processes related to containers including exited or terminated
```
docker ps -a
```
Run the container in interactive mode
```
docker container run -it --name ct1 ubuntu
```
```
touch f1 f2 f3
```
```
ls
```
```
exit
```
```
docker ps -a
```
Create another container in interactive mode
```
docker container run -it --name ct2 ubuntu
```
Press Crtl+P+Q to switch the terminal to Docker Host.
```
docker ps
```
Execute commands in an active container
```
docker container exec -it ct2 /bin/sh
```
List all the processes in the container.
```
ps all  #Or ps aux
```
```
exit
```
```
docker ps
```
Attach to the running container. Note that when you attach,  the primary process is triggered but when you exec again a new process is triggered. This can be checked by using `ps all`
```
docker container attach ct2
```
```
exit
```
```
docker ps
```
```
docker ps -a
```
Run container in detach mode
```
docker container run -d --name ct4 nginx
```
```
docker ps -a
```
```
docker container exec -it ct4 /bin/bash
```
```
apt update && apt install -y wget curl
```
```
apt install procps
```
```
ps aux
```
```
exit
```
```
ps aux
```

### Task 3: Port Mapping from Docker Host to container
```
docker run -d -p 8080:80 httpd
```
```
docker ps
```
```
docker exec -it < replace container id/name > /bin/bash
```
```
exit
```
```
docker ps
```
```
docker exec -it < replace container id/name > /bin/bash
```
```
kill 1
```
```
docker ps -a
```
```
docker container stop < replace container id/name >
```
```
docker container rm < replace container id/name >
```
```
docker image ls
```
```
docker image rm < replace image id >
```

---------------------------------**End Of Lab 2**---------------------------------
## Lab-3: Docker container life cycle

### Task 1: Docker Lifecycle 
Pull Docker Image
```
docker pull httpd
```
List all images available in Local Repo
```
docker image ls
```
Check the history of the image
```
docker image history httpd
```
Create container
```
docker container create httpd
```
List all containers
```
docker container ls -a
```
Start the created container
```
docker container start < container id/name >
```
```
docker container ls
```
Stop the created container
```
docker container stop < container id/Name >
```
```
docker container ls -a
```
```
docker container start < container id/Name >
```
Pause the container
```
docker container pause < container id/Name >
```
```
docker container ls -a
```
Unpause the container
```
docker container unpause < container id/Name >
```
```
docker container ls -a
```
```
docker exec -it < container id/name > /bin/bash
```
```
cd htdocs
```
```
apt update
```
```
apt install wget -y
```
```
rm index.html
```
```
wget https://s3.ap-south-1.amazonaws.com/files.cloudthat.training/devops/docker-essentials/index.html
```
```
exit
```
Save the container as an image 
```
docker commit < replace container id/name > myhttpd:version
```
```
docker image ls
```
Create a new container with the newly created image
```
docker run -d -p 8080:80 myhttpd:version
```
```
curl < public IP>:8080  #Public IP of your host machine
```
```
docker container ls
```
Check the logs of the container
```
docker logs < container id/name >
```
Monitor real-time resource usage for running Docker containers

docker stats         # Shows usage statistics for only running containers

docker stats -a      # Shows usage for all containers
```
docker stats < container id/name > 
```
```
docker container ls
```
```
docker stop < replace container id/name >
```
Remove a stopped container
```
docker container rm < replace container id/name > 
```
Remove a running container 
```
docker container rm < replace container id/name > -f
```
```
docker image ls
```
```
docker image rm < replace image id/name > < replace image id/name >
```
```
docker image ls
```
```
docker image ls -a
```

---------------------------------**End Of Lab 3**---------------------------------
## Lab-4:  Bind Mount in Docker

### Task 1: Starting Docker Containers Bind Mounts
```
mkdir /home/ubuntu/share
```
```
echo 'Hello From Docker Host' > /home/ubuntu/share/index.html
```
```
docker run -it --name container1 -p 80:80 -v /home/ubuntu/share:/var/www/html ubuntu:18.04 /bin/bash
```
```
apt-get update -y && apt-get install apache2 -y
```
```
service apache2 start
```
```
service apache2 status
```
```
curl localhost:80
```
```
echo 'Hello From Container1' > /var/www/html/index.html
```
```
curl localhost:80
```
Press Ctrl+P+Q, to switch back to Host
```
docker inspect container1
```
Check for keyword `Mounts`
```
docker run -it --name container2 -v /home/ubuntu/share:/var/www/html ubuntu:18.04
```
```
echo 'Hello From Container2' > /var/www/html/index.html 
```
```
exit
```
```
docker ps -a
```
```
docker rm -vf container1 container2 
```
```
cat /home/ubuntu/share/index.html
```

### Task 2: Create a bind mount with --mount option and verify it
```
docker run -d -it --name container3 --mount type=bind,source=/home/ubuntu/share/,target=/app nginx:latest
```
```
docker inspect container3
```
```
docker exec -it container3 bash
```
```
cd app && ls
```
```
cat index.html
```
```
echo "hello from container3" > index.html
```
```
exit
```
```
cd /home/ubuntu/share/
```
```
cat index.html
```

---------------------------------**End Of Lab 4**---------------------------------

## Lab-5: Bind Mount in Docker

### Task 1: Starting Docker Containers Bind Mounts
```
mkdir /home/ubuntu/share
```
```
echo 'Hello From Docker Host' > /home/ubuntu/share/index.html
```
```
docker run -it --name container1 -p 80:80 -v /home/ubuntu/share:/var/www/html ubuntu:18.04 /bin/bash
```
```
apt-get update -y && apt-get install apache2 -y
```
```
service apache2 start
```
```
service apache2 status
```
```
curl localhost:80
```
```
echo 'Hello From Container1' > /var/www/html/index.html
```
```
curl localhost:80
```
Press Ctrl+P+Q, to switch back to Host
```
docker inspect container1
```
Check for keyword `Mounts`
```
docker run -it --name container2 -v /home/ubuntu/share:/var/www/html ubuntu:18.04
```
```
echo 'Hello From Container2' > /var/www/html/index.html 
```
```
exit
```
```
docker ps -a
```
```
docker rm -vf container1 container2 
```
```
cat /home/ubuntu/share/index.html
```

### Task 2: Create a bind mount with --mount option and verify it
```
docker run -d -it --name container3 --mount type=bind,source=/home/ubuntu/share/,target=/app nginx:latest
```
```
docker inspect container3
```
```
docker exec -it container3 bash
```
```
cd app && ls
```
```
cat index.html
```
```
echo "hello from container3" > index.html
```
```
exit
```
```
cd /home/ubuntu/share/
```
```
cat index.html
```

---------------------------------**End Of Lab 5**---------------------------------
