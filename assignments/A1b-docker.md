---
layout: page
title: Assignment 1B
tagline: Docker
description: First steps using Docker
---

# Docker Environment

We will use [Docker](https://www.docker.com/what-docker) to remove the burden on unifying working environments.

## Introduction

First, go over the [basic tutorial](https://docs.docker.com/get-started/) to gain familiarity with Docker usage.
(Do not follow the instruction to install docker _yet_.)

The easiest solution is to use Docker on the computers in the terminal room; the only drawback that you
have to be in the terminal room to boot the machine in Linux (note that you can use `ssh` once it is booted, but,
anyone can decide to reboot the machine, and all machines are shutdown at the end of the day).

Alternatively, install Docker on your own laptop or home computer.
While this route is **not officially supported**, I will provide a few pointers to get you started, see below.

## Setting up Docker

Docker can be used in terminal rooms HG00.027 and HG00.075.

You need to be added to the Docker group - in theory, this has already been done, check using the `groups` command.

_If not, let me or the TAs know, or ask at CNCZ (where you received your science login)._

## Using Docker

A minimal test shows that the docker client can start so-called containers:

    docker run hello-world

If Docker is new to you, it is highly recommended to learn more about its architecture and usage on the Docker
site; specifically, the rest of the course material will assume that you followed steps **two** and **three** 
from the excellent documentation.

Follow the tutorial [**step two**](https://docs.docker.com/get-started/part2/).

In the course, we will only use docker with images provided by others, so it is not necessary to continue to 
steps three and beyond, although I will not stop you if you are starting to get the hang of it!

_Continue only after having seen the ASCII art using your own setup!_

### DIY

If you opt to install docker on your own hardware (and work independently from the availability of
computers in the Huygens building), follow the instructions for the right [Docker Community Edition](https://www.docker.com/community-edition).

_If you have an older version of Windows, you may need to use [Docker Toolbox](https://docs.docker.com/toolbox/overview/).
An alternative would be to use a virtual machine with, e.g., Ubuntu, and install Docker there._

## Scala

The practical assignments aim to give you basic knowledge of Spark, at the moment the _de facto_ Big Data platform.
We will use Spark from Scala, a functional language that is executed on the Java Virtual Machine (JVM), 
so usage of Java libraries can be mixed with pure Scala in a hybrid environment.

The usefulness of Docker is immediately clear when you explore the language and practice your Scala!
Just run a Docker container that comes with a complete Scala environment pre-installed:

```
docker run -it --rm williamyeh/scala
```

The container starts up by automatically running the Scala interpreter (or REPL). Of course, you can first start a shell in that container, by appending `/bin/bash` to the command above;
then start a Scala interpreter using `scala` from the commandline.

Links to explore:

* [Main Scala site](http://scala-lang.org/) and [documentation](http://docs.scala-lang.org/)
* [Scala tutorial for Java Programmers](http://docs.scala-lang.org/tutorials/scala-for-java-programmers.html)
* [API documentation](https://www.scala-lang.org/api/current/)

_The course is not about functional programming, so do not get carried away - you only want to acquire a basic understanding of the language._

<!--

TO BE DONE

## Spark Notebook

In the assignments, we get hands-on experience with [Spark Notebook](http://spark-notebook.io).

### Setup (first time only)

If this is the first time that you will start Spark Notebook, you need to use its image and initialize a container:
follow the instructions given in [Spark Notebook for the big data course](../background/spark-notebook.html).

### Starting the Spark Notebook container

Otherwise, start up a container with `docker run` (only if it is not running of course);
and simply open [localhost:9001](http://localhost:9001/) in your browser.

If you successfully started the Spark Notebook container, then opening [localhost:9001](http://localhost:9001/) will
show you the Spark Notebook UI in the browser. 

_Why don't you try out some of the scala things you worked with in the first week!_

(It is possible to run the docker container remotely, and open the Spark Notebook in a browser on your laptop, provided
that you know how to tunnel ports 4040 and 9001 to the laptop; for example using `ssh -L` or the right tunneling 
settings to `Putty`.)

-->

## Clean up

Once you are fluent in using the docker client, it is easy to forget that every container and image used takes up 
disk space on the local machine. Please clean up regularly!

The following command lists the running containers:

    docker ps -f status=running

Any running containers you do not use, can be stopped using `docker stop HASH`.
Next, you may remove all inactive, exited containers that you do not plan to restart by issuing one shell command:

    docker ps -f status=exited -q | \
      xargs docker rm

## See also

Optional extra reading (not required for the course):


* [Docker for Data Science](https://towardsdatascience.com/docker-for-data-science-4901f35d7cf9) (blog post)
* Advanced Docker with the [Docker book](http://www.dockerbook.com/) (not free, ~EUR 10).
