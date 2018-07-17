#### Setting Up Magento 2 and Varnish Cache on Multi-container Architecture Using Docker-Compose tool

This repository corresponds to architecture setup as mentioned in blog https://cloudkul.com/blog/magento-2-and-varnish-cache-integration-with-docker-compose/.


##### Docker-Compose Tool

As mentioned in Docker docs, Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a Compose file to configure your application’s services. Then, using a single command, you create and start all the services from your configuration. 

With the help of docker-compose we can define containers to be built, their configuration, links, volumes, ports etc in a single file and it gets launched by a single command. We can add multiple servers and services just by adding them to docker-compose configuration file. This configuration file is in YAML format.

Getting started with docker-compose is a few steps process:

> Create a Dockerfile defining the application environment. We can create separate Dockerfile for our different services. As Dockerfile are lightweight, so our application can be replicated anywhere.

> Create a docker-compose.yml file defining services that needed for application run. We can define volumes to be mapped, ports to be exposed, links to be created, arguments to be passed etc in our docker-compose.yml file.

> Run ‘docker-compose build’ to create Docker image. After creating Dockerfile, docker-compose.yml and placing our volumes at right places, we can create our image.

> Run ‘docker-compose up -d’ to run the docker containers. After image build up, we can run all of our containers as mentioned in configuration files by this single command.

##### Dockerizing Magento 2 and Varnish Cache with Docker-Compose

Docker is an open-source project that can be integrated with almost all the applications allowing scope of isolation and flexibility. It can be integrated with Magento 2 as well. Magento is an e-commerce platform written in PHP and based on zend framework available under both open-source and commercial licenses.

Varnish cache is a web application accelerator also known as a caching HTTP reverse proxy. Varnish cache visits your server once to cache the page, then all future requests for the same page will be served by Varnish cache. Varnish acts a reverse proxy server that directs client requests to the back-end apache2 server. Whenever a client makes a request, Varnish server checks the content within the cache and in case data not found, it sends the request to backend server and fetch the content to client and keep a copy of the data as cache. When the same request is made, Varnish does not bother apache2 server, it just fetch the data from the cache. It provides an additional level of abstraction and control to ensure the smooth flow of network traffic between clients and servers.

Magento 2 works out of box with Varnish Cache and provides its own VCL file for its setup. Also from Magento 2 docs, “We strongly recommend you use Varnish in production. The built-in full-page caching (to either the file system or database) is much slower than Varnish, and Varnish is designed to accelerate HTTP traffic.”

In this project, we are using:

> Operating system: Ubuntu 16.04

> Web Server: Apache2

> Database Server: Mysql-server-5.7

> Cache Server: Varnish 4.1

> PHP version: PHP-7.1

To begin with, please install docker and docker-compose on your ubuntu server. 

Then follow the following steps:

1). Clone or download this repository as 

> git clone https://github.com/webkul/magento2-varnish-docker-compose.git

2) Set mysql root credentials and name of the database to be created in ~/magento2-varnish-docker-compose/docker-compose.yml.

> mysql_password=

> mysql_database=

3). Download Magento 2 version you wish to dockerize and upload it in directory magento2 in parallel docker-compose.yml.

> Go to https://magento.com/tech-resources/download? .

4). Build the docker image.

> docker-compose build

5). Check the built image as:

> docker images

6). Run the containers from built image as:

> docker-compose up -d

7). Check the running docker containers by command:

> docker-compose ps

> docker ps

Now, your server setup is all ready, now hit your domain name or IP to install Magento 2.

Now to configure Varnish for Magento 2 and test its working, please refer to blog https://cloudkul.com/blog/magento-2-and-varnish-cache-integration-with-docker-compose/.

After configuring Magento 2 for Varnish, go to varnish docker container as

> docker exec -ti varnish bash

And run the command,

> varnishhist

#### GETTING SUPPORT

If you have any issues, contact us at support@webkul.com or raise ticket at https://webkul.uvdesk.com/
