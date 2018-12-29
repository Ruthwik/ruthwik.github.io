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
In the previous post, we saw the basic commands to create a docker image. In this post we will look at docker remote api's.
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

If there is a service with <code>/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:2375 </code> then the next steps can be skipped. Generally for the first time it has to be configured and the output looks like </li>

<img src="/img/dockerremoteapi/docker_deamon.png" alt="docker_deamon"/>

	<li> Then navigate to /lib/systemd/system in the terminal and edit docker.service file vi /lib/systemd/system/docker.service 
		<pre><code>vi /lib/systemd/system/docker.service </code></pre>
	</li>
	<li> Find the line which starts with ExecStart and adds -H=tcp://0.0.0.0:2375 to make it look like ExecStart=/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:2375 </li>

	<img src="/img/dockerremoteapi/docker_service.png" alt="docker_service"/>



	

	<li> Reload the docker daemon
			
	</li>
	<pre><code>systemctl daemon-reload </code></pre>
		<li> Restart the container
			
	</li>
	<pre><code>sudo service docker restart </code></pre>
		<li> The last step is to check whether the changes are reflected using the same command
			
	</li>
	<pre><code>ps -ef | grep docker</code></pre>
		<img src="/img/dockerremoteapi/docker_service_after.png" alt="docker_service_after"/>
	
</ul> 
</p>

> The -H flag binds dockerd to a listening socket, either a Unix socket or a TCP port. You can specify multiple -H flags to bind to multiple sockets/ports. The default -H fd:// uses systemd's socket activation feature to refer to /lib/systemd/system/docker.socket.


<h3>How to use Docker Remote API</h3>

<p>
Now that we enabled Docker remote api, it's time to dirty our hands with the api's. Here are few  
</p>

<h4>1. List of images</h4>
<p>
In the first example, I will use three different ways to fetch the list of images available on the docker machine this helps to understand the analogy between different ways.


<ul>
	<li> <strong><em>Using cmd :</em></strong></li>
	<pre><code>docker images</code></pre>
	<img src="/img/dockerremoteapi/get_images_cmd.png" alt="get_images_cmd"/>
	
	<li> <strong><em>Using curl :</em></strong></li>
	<pre><code>curl http://localhost:2375/images/json</code></pre>
	<img src="/img/dockerremoteapi/get_images_curl.png" alt="get_images_curl"/>
	
	<li> <strong><em>Browser :</em></strong> This is same as the last one but the limitation is only GET requests can be used. In order to use POST requests another client like postman is needed</li>
	<img src="/img/dockerremoteapi/get_images_ui.png" alt="get_images_ui"/>

</ul>
</p>

<h4>2. List of containers</h4>
<p>
This is to get list of containers created on the docker machine.
<pre><code>curl http://localhost:2375/containers/json?all=1</code></pre>

<img src="/img/dockerremoteapi/list_of_containers.png" alt="list_of_containers"/>

</p>

<h4>3. Pull an image</h4>
<p>
This is 
<pre><code>curl -XPOST http://localhost:2375/images/create?fromImage=tomcat:9.0</code></pre>


<img src="/img/dockerremoteapi/pull_image.png" alt="pull_image"/>


</p>

<h4>4. Create a container</h4>
<p>
When running a container via the command line you would use the docker ‘run’ command. This is a composite command, consisting of the commands ‘create’ and ‘start’.
The remote API does not support the ‘run’ command. You have to execute ‘create’ and ‘start’ separately.

<pre><code>curl -X POST -H "Content-Type: application/json" http://localhost:2375/containers/create -d '{
>       "Image":"tomcat:9.0",
>       "PortBindings": { "8080/tcp": [{ "HostPort": "9090" }] }
>  }'</code></pre>

This will give an id as output which is used to uniquely identify the container. We use this to start, stop and delete..The port bindings will map the image internal port to external port. Here tomcat's 8080 port is mapped to 9090 port. Now the tomcat is accessable on the 9090 port  of the machine. 
<img src="/img/dockerremoteapi/tomcat_container_create.png" alt="tomcat_container_create"/>


</p>

<h4>5. Start a container</h4>
<p>
Here we give the unique id in the path to start the container
<pre><code>curl -XPOST http://localhost:2375/containers/0be90b6cfec41e89270bab7280b9691773c949f6130f8aaba20dbf2aec533dcf/start</code></pre>


<img src="/img/dockerremoteapi/tomcat_container_start.png" alt="tomcat_container_start"/>


</p>

<h4>6. Stop a container</h4>
<p>
Stop the container using the container id.
<pre><code>curl -XPOST http://localhost:2375/containers/0be90b6cfec41e89270bab7280b9691773c949f6130f8aaba20dbf2aec533dcf/stop</code></pre>

</p>

<h4>7. Kill a container</h4>
<p>

<pre><code>curl -XPOST http://localhost:2375/containers/0be90b6cfec41e89270bab7280b9691773c949f6130f8aaba20dbf2aec533dcf/kill</code></pre>

</p>

I have used the following references and sometimes used the same explanation. Do check the following resources for more understanding.
 
	<ul>
      <li><a href="https://stackoverflow.com/questions/43800339/how-to-build-an-image-using-docker-api
">How to build an Image using Docker API?</a></li>
      <li><a href="https://docs.docker.com/engine/api/v1.24/
">Offical Docker documentation</a></li>
      <li><a href="https://stackoverflow.com/questions/41944550/using-the-docker-rest-api-to-run-a-container-with-parameters?noredirect=1&lq=1">
Using the Docker REST API to run a container with parameters</a></li>
	  <li><a href="https://blog.flux7.com/blogs/docker/docker-tutorial-series-part-8-docker-remote-api">Docker Tutorial Series, Part 8: Docker Remote API</a></li>
	  <li><a href="https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker">Cannot connect to the Docker daemon at unix:/var/run/docker.sock. Is the docker daemon running?
</a></li>
  	</ul> 
</p>

<p>If you have any question or feedback, please do reach out to me by commenting below.</p>

