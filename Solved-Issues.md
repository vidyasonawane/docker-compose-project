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

