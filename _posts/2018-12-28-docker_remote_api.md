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
<img src="/img/dockerremoteapi/docker_core.jpg" alt="docker_core" height="50%" width="50%">


<p>
Let's learn about the layers starting from the core

<ul>
	<li> <strong><em>Docker Daemon :</em></strong> is a service that runs on the host operating system. It currently runs on Linux because it depends on a number of Linux kernel features </li>
	<li> <strong><em>REST API :</em></strong> tools can talk to Docker daemon through the REST API exposed by the docker </li>
	<li> <strong><em>Docker CLI :</em></strong> It is a command line tool that can talk to docker daemon(This internally calls REST API exposed by docker daemon). Docker CLI comes
along with docker daemon when docker is installed </li>

</ul>
</p>

<p>
The Docker architecture is anologous to client-server architecture. The daemon is the server and the CLI is one of many clients.
</p>

<img src="/img/dockerremoteapi/docker_steps.png" alt="docker_steps"/>

<p>
Now let's look at each component of a docker ecosystem : 

<ul>
	<li> <strong><em>Client :</em></strong> This is where we run the docker commands. It can be CLI or REST API. We generally install CLI on our operating system to run the commands</li>
	<li> <strong><em>Docker host :</em></strong> This is typically referred to as the server running the Docker daemon. The client and daemon need not to be on the same machine </li>
	<li> <strong><em>Registry :</em></strong> Docker registry is a storage and content delivery system holding Docker images available in different tagged version. docker push and
 pull commands are used to interact with registry. We can create our own local registry if we wish to maintain. We can will explore this 
 in the later posts </li>

</ul>

<h3>Enabling Docker Remote API</h3>
<p>
The above explanation gives better intution about how Docker Remote API works. In order to enable Docker remote api on your machine (I use Ubuntu) follow the steps mentioned below


<ul>

<li>The first step is to check the running docker services. In order to do so use the following command.

<pre><code>ps -ef | grep docker</code></pre>

If there is a service with <code>/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:2375 </code> then the next steps can be skipped. Generally for the first time it has to be configure and the output looks like </li>

<img src="/img/dockerremoteapi/docker_deamon.png" alt="docker_deamon"/>

	<li> Then navigate to /lib/systemd/system in the terminal and edit docker.service file vi /lib/systemd/system/docker.service 
		<pre><code>vi /lib/systemd/system/docker.service </code></pre>
	</li>
	<li> Find the line which starts with ExecStart and adds -H=tcp://0.0.0.0:2375 to make it look like ExecStart=/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:2375 </li>

	<img src="/img/dockerremoteapi/docker_service.png" alt="docker_service"/>



	> The -H flag binds dockerd to a listening socket, either a Unix socket or a TCP port. You can specify multiple -H flags to bind to multiple sockets/ports. The default -H fd:// uses systemd's socket activation feature to refer to /lib/systemd/system/docker.socket.
	

	<li> Reload the docker daemon
			<pre><code>systemctl daemon-reload </code></pre>
	</li>
	
		<li> Restart the container
			<pre><code>sudo service docker restart </code></pre>
	</li>

		<li> The last step is to check whether the changes are reflected using the same command
			<pre><code>ps -ef | grep docker</code></pre>
	</li>
	
		<img src="/img/dockerremoteapi/docker_service_after.png" alt="docker_service_after"/>
	
</ul> 
</p>

<p>If you have any question or feedback, please do reach out to me by commenting below.</p>

