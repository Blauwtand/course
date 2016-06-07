---
layout: page
title: Self Contained Apps 
description: Run your own Spark applications written in Scala on Hathi 
---

## Running Self Contained Apps on Hathi

So far, we have only used Spark in an interactive setting, making best use of the Spark Notebook.

**You should definitely develop your project like that:
locally on your own machine using small test data, taken as samples from the real Commoncrawl.**

However, eventually, we will want to run a program on the real cluster, using the actual Web data.
Unfortunately however, using Spark interactively from Spark Notebook does not
work properly (yet?) on `hathi`, the national [Hadoop cluster](https://userinfo.surfsara.nl/systems/hadoop/description).

This instruction will get you up and running with developing _standalone_ Spark solutions that can be
executed on the cluster, assuming that you have claimed success on running the `SparkPi` example from
the Docker image provided by SurfSara.

### Preparation

First install `sbt` on SurfSara's Docker image.
Hereto, follow the instructions from [`scala-sbt.org`](http://www.scala-sbt.org/0.13/docs/Installing-sbt-on-Linux.html).

```
apt-get install apt-transport-https

echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823
apt-get update
apt-get install sbt
```

(While at it, I issued `apt-get install vim` as well, but feel free to skip this.)

### `RUBigDataApp`

Glance over the Spark project's documentation on creating 
[self-contained Spark apps](http://spark.apache.org/docs/1.6.1/quick-start.html#self-contained-applications)
to find out how to create a standalone Spark application and subsequently run the application using 
[`spark-submit` for a yarn cluster](http://spark.apache.org/docs/1.6.1/running-on-yarn.html#launching-spark-on-yarn).

The official documentation is a little too concise to be very useful, so let us walk through the process with an actual (but _overly simple_) 
example of a Spark application written in Scala.

Download compressed archive [`rubigdata.tgz`](rubigdata.tgz) from the course website into your Docker container, and unpack the archive.

```
cd /hathi-client/spark
wget http://rubigdata.github.io/course/assignments/rubigdata.tgz
tar xzvfp rubigdata.tgz
cd rubigdata
```

Now, we copy a small text file into your home directory on the cluster; feel free to first modify the sample textfile before copying it to HDFS.

```
hdfs dfs -put rubigdata-test.txt
```

Build the stand-alone application (_do not forget to first inspect the code, so you know what to expect!_)
The two inputs to this process are the `rubigdata.sbt` file and the actual code provided in `rubigdata.scala`.
The directory structure provided through the compressed archive is important; 
for the details, look into the `sbt` documentation.

```
sbt package
```

The result is a `jar` file that we can execute on `hathi` using Spark's `spark-submit` command:

```
spark-submit --master yarn --deploy-mode cluster /hathi-client/spark-1.6.1-bin-hadoop2.6/rubigdata/target/scala-2.11/rubigdataapp_2.11-1.0.jar
```

Follow the output by opening the URL that is given on `stdout` 
(this URL looks like `http://head05.hathi.surfsara.nl:8088/proxy/application_1458320004153_68201/`).

While the application runs, you will see the already familiar Spark UI (visible in standalone mode at `localhost:4040`); 
once the application is finished, you get a summary page, from which you can inspect the logs.
In our simple example program, these logs contain the output: character counts in the textfile we stored in our home directory on HDFS.

### Next steps

Before trying to analyze Commoncrawl data, I suggest to run a few spark exercises from [assignment 2a](A2a-spark-101.md) 
and [assignment 2b](A2b-execution-model.md). You can save any notebook as just its Scala code by using the _save as_ option
from the file menu.

_Include a brief discussion, perhaps using a concerete example, in the introductory part of your blog post, 
taking your readers along on the road from interactive small scale prepatory experiments to actual use of a large cluster._