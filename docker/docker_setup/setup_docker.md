Here's the provided text converted into Markdown format:


# How to Install Docker on Linux Mint 21 Step-by-Step

**Published on: June 25, 2024 by Anirban Mukherjee**

In this blog post, we will show you how to install Docker on a Linux Mint 21 system step-by-step.

Docker is an open-source tool that allows developers and system administrators to package their applications along with all dependencies inside a Docker image. Later, this image can be distributed among team members and can run a container using this image where Docker is installed.

Docker comes in Community Edition and Enterprise Edition. In this post, we will be installing Docker Community Edition.

## Table of Contents
- Prerequisites
- 1) Install Docker Dependencies
- 2) Import Docker GPG Key
- 3) Add Docker APT Repository on Linux Mint 21
- 4) Install Docker on Linux Mint 21
- 5) Manage Docker with Local User
- 6) Test Docker Installation

## Prerequisites
- Pre-Installed Linux Mint 21 System
- Sudo User with admin rights
- Reliable Internet connection

Without any delay, let’s jump into Docker installation steps.

### 1) Install Docker Dependencies
Open the terminal and run the following `apt` commands to install Docker dependencies.

```bash
$ sudo apt update
$ sudo apt install -y apt-transport-https ca-certificates curl gnupg
```
![Install Docker Dependencies on Linux Mint 21][<img src="./docker-svgrepo-com.svg" width="15"/>](./docker-svgrepo-com.svg)

### 2) Import Docker GPG Key [<img src="./docker-svgrepo-com.svg" width="15"/>](./docker-svgrepo-com.svg)
Run the following `curl` command to download and import the Docker GPG key into your Linux Mint 21.

```bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/dockerce.gpg
```


### 3) Add Docker APT Repository on Linux Mint 21
Now, add the following APT repository for Docker on your Linux Mint 21, run the below `echo` command:

```bash
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/dockerce.gpg] https://download.docker.com/linux/ubuntu jammy stable" | sudo tee /etc/apt/sources.list.d/dockerce.list > /dev/null
```
![Add Docker APT Repository on Linux Mint 21][<img src="./docker-svgrepo-com.svg" width="15"/>](./docker-svgrepo-com.svg)

Next, update the package index by executing the command below:

```bash
$ sudo apt update
```

### 4) Install Docker on Linux Mint 21
As we have completed all prerequisites, now it’s time to install Docker. Run the following `apt` command:

```bash
$ sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
This command will install the latest version of the Community Edition of Docker.

![Install Docker on Linux Mint 21][<img src="./linux-mint.svg" width="22"/>](./linux-mint.svg)

Once Docker and other required packages are installed, verify the Docker version and its service.

```bash
$ sudo docker version
```
![Check Docker Version on Linux Mint 21][<img src="./linux-mint.svg" width="22"/>](./linux-mint.svg)

```bash
$ sudo systemctl status docker
```
![Docker Service Status Check on Linux Mint 21][<img src="./linux-mint.svg" width="22"/>](./linux-mint.svg)

Perfect, the output above confirms that the Docker service is up and running.

### 5) Manage Docker with Local User
If you want your local user to manage Docker, you need to add the user to the Docker secondary group. Run the following `usermod` command:

```bash
$ sudo usermod -aG docker $USER
$ newgrp docker
```

Now, you can run Docker commands without typing `sudo` in front of it.

### 6) Test Docker Installation
To ensure that Docker is installed correctly on your Linux Mint 21 system, you can run a container using the `hello-world` image as shown below:

```bash
$ docker run hello-world
```
![Docker Run Hello World on Linux Mint 21][<img src="./docker-svgrepo-com.svg" width="15"/>](./docker-svgrepo-com.svg)

This command will download the `hello-world` image and run a container from it. If everything is set up properly, you will see an informational message confirming that Docker is working correctly.

That’s all from this post. We believe you have found it informative and useful. Please do post your queries and feedback in the comments section below.
```