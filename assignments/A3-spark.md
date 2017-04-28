---
layout: page
title: Spark
tagline: Hands-on session with Spark RDDs, SQL and DataFrames
description: Use the different Spark APIs in practice and understand their inner workings.
---

Assignment 3 consists of two parts that focus on query processing and data analysis with Spark,
using the core RDD API as well as the newer and more high-level DataFrames.

You accept the assignment via Github for Education, using 
[__this invitation link__]().

### Blog Post

The assignment is to write a blog post about your experience with Spark.

While assignment 3A looks into RDDs, the data representation and query processing internals of using Spark,
assignment 3B is focused on the use of Dataframes and Spark SQL. It is up to you to choose the preferred angle
for your blog post: you may focus on the Spark internals where the emphasis is assignment 3A (looking into the
details of query processing in Spark, perhaps using some of the queries in the 3B notebook to illustrate your
point) or it is assignment 3B (focusing more on the analytical side, by analyzing a different dataset).
Whatever you choose, include in your blog post the insights you gain from inspecting the Spark UI after
issuing commands from the notebooks.

#### Option A

Interesting aspects you might want to address include the lazy evaluation, the effect of caching RDDs,
partitioning of the RDDs, etc. Ideally, you would experiment with a few alternative solutions for the same
high-level objective, and/or different choices in the setup of the dataset (like number of partitions, how
to avoid shuffles, relationship between number of shuffles and overall processing cost, etc.).

#### Option B

The most basic version for a blog post from the angle of assignment 3B would be to continue the analysis of the
data we already used in the notebook. Can you provide a more complete list of dated quarters or improve the estimated
dates? Include different data, or answer a different question about this data?

Alternatively, you could decide to carry out a small analysis of a different open dataset, of your own choice;
and present to your readers some basic properties of that data. _You will notice that it is harder than following
instructions, and you run the risk of getting stuck because the data does not parse well, etc._

As a third and final suggestion, the assignment repo gives you three different datasets that you can use to solve
a task I recently encountered myself, in the context of the organization of the ACM SIGIR conference in 2017.
The provided data consists of the following three files:

* `SIGIR2017-invitees.csv` is the spreadsheet we used in September to invite committee members;
* `committee.csv` is a recent (April) dump of the committee member metadata from the conference system we use;
* `committee_topic.csv` contains additional information about the committee members' interest.

We would like to pass on the original spreadsheet to the PC Chairs of SIGIR 2018, because it has a pointer to
their DBLP page (basically their CV). However, some of the PC members have moved institute, or changed their
contact details like email address; this is only reflected in the dump of the conference system.
Perhaps we would also want to enrich the data to be passed on with additional columns like personal webpage
and topics of interest.

The assignment for you would then be to (use Spark to) combine the three datasets into a new integrated dataset
that we could hand over to the 2018 chairs. Your blog post would discuss the choices you make (I would expect
that the blog post is supported by a new Spark Notebook that you should push to the assignment repo).

### Done

When you completed the assignment, push your blog post to the first assignment's repository
(in the `gh-pages` branch or it will not render).

and include a link to the published blog post in the README of the third assignment repository.
Push the updated README as well as your own code or notebook to the third assignment repository.

### Help?!

Feel free to ask for help, but please do that by using the github issue tracker on [the forum](https://github.com/rubigdata/forum-2017/); 
see the [welcome issue](https://github.com/rubigdata/forum-2017/issues/1) as an example of how to proceed.
Every student may help out, please contribute and share your knowledge! 

[Back to assignments overview](../index.html)


