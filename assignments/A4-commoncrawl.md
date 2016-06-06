---
layout: page
title: Assignment 4 
description: Commoncrawl
---

## Commoncrawl

Assignment 4 is an open assignment, where we will work with data on the national supercomputer infrastructure managed by SurfSara.

We have to see how far we get - the main objective is not so much to prepare a winning submission for the next Norvig Award, but 
merely to get hands-on experience in running _and debugging_ jobs on a shared managed cluster, instead of our own laptops or
desktops (that at best emulate a real cluster, and in the worse case will mislead you to underestimating the problems of working 
on actual __Big Data__).

### Preparations

We work on the national [Hadoop cluster](https://userinfo.surfsara.nl/systems/hadoop/description).
Instead of following the _Obtaining an account_ instructions, you have to receive your account info from me.

#### Initial setup

Let us work through the basics discussed on the
[Hadoop cluster usage page](https://userinfo.surfsara.nl/systems/hadoop/usage).

Start by using the provided docker image.

```
docker pull surfsara/hathi-client

docker run -it surfsara/hathi-client
```

#### Kerberos authentication

Because the national cluster serves many users that not all have access to the same data, authentication is kind-a strict, provided
through MIT's Kerberos.

Inside a Docker container, this works smoothly: 
use your credentials (obtained from me) to get a Kerberos ticket, 
by following the [SurfSara instructions](https://userinfo.surfsara.nl/systems/hadoop/usage).

To authenticate through Kerberos _on a Linux or Windows machine_ **outside** the Docker image,
which will be necessary to use the ResourceManager from your web-browser, 
please [follow these steps](kerberos.html) (provided without warranty, by me).

#### First steps on Hathi

Try a simple directory listing of the most recent crawl:

```
hdfs dfs -ls /data/public/common-crawl/crawl-data/CC-MAIN-2016-07
hdfs dfs -ls -h /data/public/common-crawl/crawl-data/CC-MAIN-2016-07/segments/1454702039825.90/warc
```

#### Setting up Spark environment

Spark Notebook is not supported on the national hadoop cluster, but Spark is.

Next, let us go through the basics of running a Spark job on the cluster.
Quickly scan the [Surfsara specific instructions](https://userinfo.surfsara.nl/systems/hadoop/software/spark);
to install Spark on the docker image, proceed however with the specific instructions given here:

```
cd hathi-client
perl -e 's/version=1.6.0/version=1.6.1/g' -npi bin/get.sh
perl -e 's/spark-assembly-1.6.0/spark-assembly-1.6.1/g' -npi conf/spark/spark-defaults.conf
bin/get.sh spark
```

From now on, initialize the right environment for working with Spark by issuing the following command:

```
bin/env.sh
```

Copy-paste the printed `export` commands that set environment variables into the shell.
Then try out the standard example to compute Pi through a random process. 
(The SurfSara cluster requires jobs to be submitted through `yarn`.)

```
cd spark
MASTER=yarn-cluster bin/run-example SparkPi
```

If you managed to get a Kerberos ticket and configured your Firefox correctly, you can view
the application state in the Resource Manager, very similar to this screenshot:
![ResourceManager](screenshot-hathi-resourcemanager.png)

If this succeeded, we are ready for using the cluster for real!

#### Using Spark on the cluster

Before moving on the final project work, carry out the course instructions on 
[executing self-contained Spark applications](sbt.html).
This helps you run a simple Spark application on the cluster from inside your 
SurfSara Docker container.

### Assignment

Now that you got this far, it is time to be creative and modify the setup and files provided 
for your own project's sake.

The assignment is very open-ended: 
"do something with the Commoncrawl data" and write-up your experience in a final blog post.

#### Blog post 

Imagine a reader that has followed your previous experiences with Spark.
The goal of this post is to share your work on the Commoncrawl data with them,
emphasizing the differences between running locally a prepared notebook versus
a real project on a more unfamiliar remote environment.

Readers will be curious to learn basic statistics about the crawl, but also how
long it takes to make a pass over the data, both on average, and under peak loads.

Ideally, your analysis teaches us something about the Web we did not yet know;
but that is not a requirement for completing the assignment.

_Wishing you good big data vibes!_

Oh, and do not forget:
**use Piazza to find help from your fellow students and/or me!**
