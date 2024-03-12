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
End Of Lab 1
