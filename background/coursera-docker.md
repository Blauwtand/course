---
layout: page
title: Using the Coursera Docker Image
description: How to use the Coursera Docker Image on the machines in the Huygens terminal rooms
---

# Coursera Docker Image

## Setup

Make sure to have first read [Docker instructions](docker.html).

Then initialize the Cloudera docker image, as follows:
 
## Setup Cloudera docker image in terminal rooms

    docker import - cloudera/quickstart:latest < /vol/practica/BigData/cloudera-docker-image.tar
    docker load < /vol/practica/BigData/cloudera-docker-image.tar

## Setup Cloudera docker image at home

    docker pull cloudera/quickstart:latest

## Start the Cloudera docker image

When running the image (i.e., starting a container), we will request the web interface to be exposed (port 80) so you can follow the tutorial using your local browser.

    docker run --hostname=quickstart.cloudera --privileged=true --name=CDH -t -i -p 80 docker.io/cloudera/quickstart /usr/bin/docker-quickstart

Using the `-i` option opens an interactive shell, `-t` creates a pseudo-TTY. 
You can detach the terminal with key sequence `Ctrl-p``Ctrl-q`.

Get the exposed port using `docker ps` and a subsequent `docker port HASH`. If you assigned a name to a container, e.g. giving option `--name=CDH`, 
then subsequent commands can use the given name instead of its hash, e.g., `docker port CDH`.

## Using Cloudera docker image

Follow the tutorial on http://localhost/

The original tutorial data is stored in a relational database that you can access as follows:

    mysql --user=retail_dba --password=cloudera  retail_db

*Etc.*

## Clean up

When we complete the first phase of the course (in April), we will not use the cloudera image any more.
Remove the cloudera image as follows:

    docker images -q docker.io/cloudera/quickstart | \
      xargs docker rmi

