---
layout: post
title: Installing Docker Compose
subtitle: Installing Docker Compose.
published: true
categories: other
tags: [docker, containerization]

bigimg:
  - /img/dockerbuild/containers.jpg

---

<p>
Wikipedia defines Docker as
</p>

> an open-source project that automates the deployment of software applications inside containers by providing an additional layer of abstraction and automation of OS-level virtualization on Linux.


<h3>What is a Docker Compose file?</h3>
<p>
Dockerfile is used to build a docker image and docker run command to run the application. While building a solution generally there will be many number of applications. What if there are hundred of them?

<code>Oh God... Please help the deployer of these applications.</code>

<strong><em>Docker-compose</em></strong> comes to our rescue. With a single command the tedious task of running each application can be done effortlessly.

Docker-compose helps to start all the applications from the provided configuration. In this post we will learn from how to install docker-compose and finally use it.

</p>

<h3>Install docker-compose</h3>
<p>
The steps from 3 show how to install docker-compose. For those who already have installed the docker-compose but want to upgrade can follow from step 1.
</p>

<h4>Step 1: Check for the version and remove</h4>


```
	docker-compose --version
```
<img src="/img/dockercompose/version.jpg" alt="docker_version" height="50%" width="50%">

```
	sudo apt-get remove docker-compose
```

<img src="/img/dockercompose/docker_remove.jpg" alt="docker_core" height="50%" width="50%">

<h4>Step 2: Download and install </h4>


```
	sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
<img src="/img/dockercompose/dockercompose_download.jpg" alt="docker_core" height="50%" width="50%">


<p>
Give all permissions
</p>

```
	sudo chmod +x /usr/local/bin/docker-compose
```



```
	sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

```
	docker-compose --version
```
<img src="/img/dockercompose/dockercompose_permission.jpg" alt="dockercompose_permission" height="50%" width="50%">


<h3>Creating the first docker-compose file</h3>
<p>
In my previous post I have mentioned how to create a hello world docker image.I will be using the same docker image in this example.
<script src="https://gist.github.com/Ruthwik/55880e193f7594f19737d010764fb214.js"></script>

Check for the hello world image using docker command.

```
	docker images

```

<img src="/img/dockercompose/images.jpg" alt="images" height="50%" width="50%">
</p>



<h4>Run docker-compose</h4>
<p>
Use this command to run the docker image. A default network is created in case we don't provide a network.
</p>

```
	docker-compose up

```
<img src="/img/dockercompose/docker_compose_up.jpg" alt="dockercompose_up" height="50%" width="50%">

<h4>Run the docker-compose in a background mode</h4>
This command help to run the containers in a silent mode.

```
	docker-compose up -d
```

<h4>Stop the running containers</h4>


```
	docker-compose down
```

<p>If you have any question or feedback, please do reach out to me by commenting below.</p>
