---
layout: post
title: Docker Remote API 
subtitle: Docker from distance.
published: true
categories: other
tags: [docker, containerization]

bigimg:
  - /img/dockerremoteapi/dockerremoteapi.jpeg

---


<p>
In the previous post Building a Docker image, we saw basic commands to create a docker image. In this post we will look at docker remote api's.
</p>

<h3>Understanding Docker Architecture</h3>
<p>
Before diving into the docker remote api's, visualizing docker architecture will give better intution. Here's a peek at how Docker works under the hood.
</p>
<img src="/img/dockerremoteapi/docker_core.jpg" alt="docker_core"/>


<p>
Let's learn about the layers starting from the core

<ul>
	<li> Docker Daemon : is a service that runs on the host operating system. It currently runs on Linux because it depends on a number of Linux kernel features. </li>
	<li> REST API : tools can talk to Docker daemon through the REST API exposed by the docker. </li>
	<li> Docker CLI : It is a command line tool that can talk to docker daemon(This internally calls REST API exposed by docker daemon). Docker CLI comes
along with docker daemon when docker is installed. </li>

</ul>
</p>

<p>
The Docker architecture is anologous to client-server architecture. The daemon is the server and the CLI is one of many clients.
</p>

<img src="/img/dockerremoteapi/docker_steps.png" alt="docker_steps"/>

<p>
Now let's look at each component of a docker ecosystem : 

<ul>
	<li> <strong><em>Client :</em></strong> This is where we run the docker commands. It can be CLI or REST API. We generally install CLI on our operating system to run the commands. </li>
	<li> Docker host : This is typically referred to as the server running the Docker daemon. The client and daemon need not to be on the same machine.. </li>
	<li> Registry : Docker registry is a storage and content delivery system holding Docker images available in different tagged version. docker push and
 pull commands are used to interact with registry. We can create our own local registry if we wish to maintain. We can will explore this 
 in the later posts. </li>

</ul>



<p>If you have any question or feedback, please do reach out to me by commenting below.</p>

