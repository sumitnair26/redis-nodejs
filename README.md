 
#  Redis
Redis is an open-source, in-memory data structure store, used as a database, cache, and message broker

One of the key features of Redis is its ability to keep all data in memory, which allows for high performance and low latency access to data.  

##  Starting redis locally
 

	 docker run --name my-redis -d -p 6379:6379 redis
     docker exec -it container_id /bin/bash
     redis-cli

##  Redis as a DB

#### SET/GET/DEL

- Setting data

	    SET name "Hello Sumit" 

- Getting data

	     GET name

-    Deleting data

	       DEL name

#  HSET/HGET/HDEL (H = Hash)

    HSET user:100 name "Sumit Nair" email "sumit.nair26@gmail.com" age "30"
    HGET user:100 name
    HGET user:100 email
	
##  Redis as a queue

You can also push to a `topic` / `queue` on Redis and other processes can `pop` from it.


-  Pushing to a queue

	    LPUSH problems 1
	    LPUSH problems 2

- Popping from a queue

	    RPOP problems
		RPOP problems 
-  Blocked pop

		BRPOP problems 0
		BRPOP problems 30
The last argument represents the timeout before the blocking should be stopped

## Talking to redis via Node.js

  
There are various `clients` that exist that let you talk to `redis` via Node.js

[https://www.npmjs.com/package/redis](https://www.npmjs.com/package/redis)

Let’s initialize a simple Node.js express server that takes a `problem submission`  as input and sends it to the queue.

Let’s also create a `worker` service that picks up a problem, waits for 2 seconds and then proceeds to pick the next one.

****To run this project locally, follow these steps:****

1. Clone the repository:

```bash

git clone https://github.com/sumitnair26/redis-nodejs

```
 - Navigate to the project directory:

	    cd  express-server

 - Install dependencies:

	    npm install

 - Run the development server:

	    tsc -b 
	    node dist/index.js

 - Go to Postman 
	 - Send Post Request to http://localhost:3000/submit
			 - Params :	

		    {   
		    	    "problemId":"1",
		    	    "code":"Some Code",
		    	    "language":"Hindi"
		    }

 - Navigate to the Worker directory:

	    cd  worker

 - Install dependencies:

	    npm install

 - Run the development server:

	    tsc -b 
	    node dist/index.js
