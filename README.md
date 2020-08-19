# trandoshan-parent

Parent repository used to centralize tools to run the application, manage source code, ...

If you want to clone all projects used by Trandoshan it can be done by issuing the following command:

``./clone.sh``

# how to bootstrap trandoshan locally?

First of all make sure docker is running, then issue the following command:

``cd trandoshan-parent/``
``./bootstrap.sh``

the command will pull image from docker hub (https://hub.docker.com/u/trandoshanio)

## How to start the dashboard?

As you may notice when running the bootstrap script the dashboard won't goes up.

This is indented because the API url use by the dashboard cannot be given at runtime (since angular is a client rendered application)

Therefore you'll have to build your own version of Dashboard with the api url correctly configured

This can be done simply by opening a terminal in the *dashboard* directory and issue the following command:

``docker build . -t trandoshanio/dashboard``

this will build a dashboard version that will be deployed the next time you run the bootstrap script.

## How to access the dashboard?

You can access the dashboard at http://localhost:15003

# How to contribute

First of all thank you! I'm really happy that people are interested about Trandoshan and I really want to build a little community around the project.

The first thing to do before coding is to build your custom dev version of trandoshan. 

To do this all you have to do is to issue the following command:

``cd trandoshan-parent/``
``./build.sh``

this will build a docker image for each projects listed in *projects.txt*

Now, when you will start a local trandoshan instance using the bootstrap script you'll bring up your custom version of Trandoshan

# How to start the crawling process?

Just uncomment the following line in *docker-compose.yml* 

```yaml
#   feeder:
#      image: trandoshanio/feeder
#      environment:
#         - NATS_URI=nats://derek:pass@messaging-server:4222
#         - INITIAL_URI=something_here
#      depends_on:
#         - messaging-server
```

and configure the *INITIAL_URI* env variable to the url you want to crawl

# Commands for operating mongoDB database
Show all running containers

``docker ps``

Open a shell to a running container

``docker exec -it <container name> bash``

Start mongoDB in the shell

``mongo``

Show current database

``db``

Show all databases on the server

``show dbs``

Show all availabel databases

``show databases``

Switch current database to <db>

``use <db>``

Show all collections of current database

``show collections``

Find all documents in the collection

``db.<collection>.find()``

Show total number of documents in the collection

``db.<collection>.count()`

Export the collection to a file

``mongoexport --db <database name> -c <collection name> --out <file path and name>``

Copy a file in the container to the host

``docker cp <container>:<file name> <host path>``

# Connect to MongoDB database in the container by MongoDB Compass
First install [MongoDB Compass](https://www.mongodb.com/try/download/compass])

Then get the IP address of MongoDB database by ``docker inspect <mongo container name>``

Finally fill in the Hostname with the IP address in MongoDB Compass and connect. The port is by default 27017.