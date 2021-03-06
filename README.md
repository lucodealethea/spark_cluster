# Docker to help us start a Spark cluster in minutes
	
	
#### What docker provides:

- A closed network subnet where the docker containers can talk to each other.
- A default gateway for the containers for outbound traffic.
- Installed images, you literally need to do nothing.
 
#### Prerequisites:

- Installed docker, docker-compose ( 1.9.0 or higher )
- Linux box (or Windows, not tested here).
    
#### Install Spark:

Create a dir at any location. This dir name, will be used for your project.

$ mkdir spark ; cd spark

Copy the current project docker-compose.yml file to yours ( or download the zip)

$ docker-compose up -d

$ docker ps


Two containers running...


#### To expand your cluster

$ docker-compose scale worker=2


$ docker ps


Three containers are running now...


#### Figure out the I.P (docker bridge ) on which the master container is running using $ docker inspect 

$ docker ps | grep master
$ docker inspect 54145407w96 | grep IPAddress

"SecondaryIPAddresses": null,
 "IPAddress": "",
 "IPAddress": "172.18.0.2"
 
 
#### Install a Spark Client on the host (why not in a dedicated container ?)

$ cd ~/Downloads
$ wget https://d3kbcqa49mib13.cloudfront.net/spark-2.1.1-bin-hadoop2.7.tgz
$ tar xvzf spark-2.1.1-bin-hadoop2.7.tgz ~/spark
$ cd ~/spark/spark-2.1.1-bin-hadoop2.7/bin

#### Connect to the master using the Spark Shell.

$ ./spark-shell --master spark://172.18.0.2:7077

