# docker-compose-project
Docker Compose with multiple local containers

### Goal:
To make a docker container that contains a web application that simply displays inside the browser, The number of times someone  visited this server/page.

In order to build this, we're going to need two separate components:
1.  web server to respond to HTTP requests and generate some HTML to show the number of times the page has been visited.
2.  redis server to store the number of times that page has been visited. this is an in-memory data store, a tiny little database that sits entirely inside of memory.

_(NOTE: we can store this number of visits inside the node application itself. That's totally an option. However just to make the thing a little bit more kind of sufficiently complicated we are going to make use of redis.)_

### How to architecture it using docker?
* __First Approach:__

  To make a single container, inside that single container we can run both, node application and a redis server.
  
* __Second Approach:__

  However if this application ever got popular to any degree it would start to have some issues. Let's imagine that you start getting a lot of traffic to this web site. You're probably going to introduce more webservers to respond to incoming HTTP requests. In order to make additional servers, you might create additional instances of your doctor container that contains both the node application and an instance of redis.
  
  the issue with this approach is that, all the redis servers in different containers will be completely disconnected from each other. And so one server may store the number as 99, some other radis instance in another container might think that its only been visited three times. So in general we would definitely not want to create multiple instances of redis for a single app.
  
  Instead, we will have one single instance of redis and then if we need to scale up the web application, we could just scale the node server and make additional instances of the notes server. We are going to have separate docker containers for both the node application and the redis server.


### Docker Compose
  A separate CLI that gets installed along with docker.
  
  __What docker composed does and what Docker CLI does and what the relationship between the two?__
    
  the purposes of Docker compose is to avoid writing all the tiny little options every time you want to start up a container.

  Docker compose makes it very easy and very straightforward to start up multiple docker containers at the same time and automatically connect them together with some form of networking. it's all going to happen behind the scenes for us quite automatically.

  The purpose of Docker compose is to essentially function as Docker CLI but allow you to issue multiple commands much more quickly.

  Bu using docker compose, Containers have free access to each other and can exchange as much information as they want without having to exchange or open up any ports between the two. Hence after using the docker compose, the first line will be `Creating network "docker-compose-project_default" with the default driver` 

* To build and run the container using docker compose, use
  `docker-compose up`
* To see the status of containers written in docker-compose.yml, run `docker-compose ps` (NOTE: run this command only inside the directory where docker-compose.yml file is present, otherwise it will give error.)

### How to stop the containers, started using docker-compose?
  In docker compose and we're working with multiple images or multiple containers at the same time. we can close them all at the same time with one single command.
  `docker-compose down`
  It will stop and remove all the containers.



