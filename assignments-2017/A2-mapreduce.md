---
layout: page
title: Map Reduce
tagline: Hands-on session with Hadoop and Map-Reduce
description: Learn how the abstract concepts from the lectures so far work out in practice.
---

Lectures 3 to 5 discussed distributed filesystems and Map-Reduce, that in practice today are almost equivalent to "Hadoop".

In this assignment, we install Hadoop on our own "pseudo-cluster", and use Map-Reduce to do some basic count operations.

You accept the assignment via Github for Education, using 
[__this invitation link__](https://classroom.github.com/assignment-invitations/aa78e0a3d4d8fd784c82239905254b9a).

The tutorial was tested inside the Docker container for Spark-Notebook that we setup in the previous lab sessions;
you would use the `docker exec` command to start a shell inside the image first:

```
docker exec -it HASH /bin/bash
```

The HDFS filesystem that you create and use in this tutorial, can be re-used in the later lab sessions on Spark.

### Setup

Start the docker container (refer to [assignment A1.b](A1b-docker.html)
and the [Spark Notebook background](../background/spark-notebook.html)
if necessary).

Setup distributed filesystem `HDFS` and the Map-Reduce tools using [__this course's Hadoop instructions__](../background/hadoop.html).

### Blog post

The assignment is to write a blog post about your experience with HDFS and Map-Reduce.

Assume the reader knows what a distributed filesystem is, and why you would use it.

Copy the *Complete Shakespeare* in text provided at 
[`/vol/practica/BigData/100.txt.utf-8`](file:///vol/practica/BigData/100.txt.utf-8)
into directory `/mnt/bigdata` in the docker container.
Alternatively, download it directly from the _Project Gutenburg_ website:

```
wget http://www.gutenberg.org/ebooks/100.txt.utf-8
```

Walk your readers through a simple Map-Reduce example to count the number of lines, words or characters 
(or something more interesting, it is really up to you).

Use the Map-Reduce documentation to get started:
[tutorial WordCount v1.0](https://hadoop.apache.org/docs/r2.7.3/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html#Example:_WordCount_v1.0)

If you clone your assignment repository, you find the example `WordCount.java` as starting point. 

Address at least the following questions:
+ What happens when you ran the commands in the _Standalone_ part of the tutorial?
+ What is different in the _Pseudo-Distributed_ case?
+ How do you use mapreduce to count the number of lines/words/characters/... in the *Complete Shakespeare*?
+ Does Romeo or Juliet appear more often in the plays?
  Can you answer this question making only one pass over the corpus?

If things go smooth, try to compute the average number of words or characters per line.

If things go _really_ smoothly, you can try to use a combiner and discuss the improvement achieved.

### Done

When you completed the assignment, push your blog post to the first assignment's repository
(in the `gh-pages` branch or it will not render);
and include a link to the published blog post in the README of the assignment repository,
and commit the README as well as your code to the assignment repository.

### Help?!

Feel free to ask for help, but please do that by using the github issue tracker on [the forum](https://github.com/rubigdata/forum-2017/); 
see the [welcome issue](https://github.com/rubigdata/forum-2017/issues/1) as an example of how to proceed.
Every student may help out, please contribute and share your knowledge! 

[Back to assignments overview](../index.html)


