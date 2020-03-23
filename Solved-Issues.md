1.  `Error: Redis connection to 127.0.0.1:6379 failed - connect ECONNREFUSED 127.0.0.1:6379
at TCPConnectWrap.afterConnect [as oncomplete] (net.js:1141:16)`

    start the redis server, using the command `docker run redis` in one terminal and run `docker run vidya25/visits` in another terminal

    It will still give the same error because there is no communication between two containers, the node app container and redis container. They are two absolutely isolated processes. So in order to make sure that the node app has the ability to reach out to the redis server and store information, we need to set up some networking infrastructure between the two.

    Options for connecting these 2 containers:
    
    1.  Make use of Docker CLI: 
    
        it's a real pain in the neck to do when you make use of CLI to set up some networking. It's going to involve a handful of different commands that we rewrite on every single time you start up your different containers.

    2.  use a separate CLI tool called **docker compose** 
    
        docker compose is a separate tool that gets installed along with docker.

        used to startup multiple docker containers at the same time.

        automates some of the long-winded arguments we were passing to `docker run`

2.  Container Maintainanace with docker-compose:

    how to deal with containers that crash for some given reason and How to essentially restart a container when the software inside of it has an air of some sort to get started.

    Specifying restart policies inside of docker compose file.
    
        1.  "no": By default we have the no restart policy assigned to all of our containers. The no restart policy means if this thing crashes for any reason do not attempt to restart the container. ( you specifically have to put it in quotes either double or single. In a YAML file, it gets interpreted as false without quotes.)
        
        2.  always: if the container stops for absolutely any reason whatsoever automatically attempt to restart it.

        3.  on-failure: only restart the running container if we get a error code.

        4.  unless-stopped: Always restart unless we (the developers) forcibly stop it.

    **Best-practices: _always versus on failure._**
    
    Always: If you're running some public web application, chances are 100 percent of the time you want that server to be available. And so if you are running some type of web application, use the always restart policy so that you are at least always attempting to keep your server running.
    
    on-failure: if you are running some type of worker process like some container that is meant to do some amount of processing on some file and then naturally exits. probably don't want to start it back up because it finished its job.







