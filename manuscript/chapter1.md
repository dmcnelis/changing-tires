# Introduction

Modern big data stores have become an essential part of many company's ability
to store, analyze and monetize their data.  Beginning with the initial release
of Hadoop in December of 2011 [^hadoopRelease] and Cassandra in 2010 [^cassandraRelease]
one of the regular challenges faced by both system administrators and software engineers
has been dealing with migrating these, and similar, systems to newer versions.

Like any software ecosystem these packages have grown considerably in a number of
key areas, primarily in terms of stability and feature sets.  Naturally, as we develop
our own systems, we are going to want to take advantage of these advances and
stand on the shoulders of those that built things before us.

The purpose of this book is to equip you with some tools and ideas on how you
can successfully move your infrastructure forward with new versions of key pieces
of your infrastructure, understanding some of the risks involved, what you can do
to mitigate your risks, how to plan for the future to make your life easier, and
suggest possible approaches that you can take.

## What can you expect in this book

The first section of this book is going to be discussing initial architectural
concepts that can make this process easier, and ways that you can start to implement
these concepts without taking a torch to all of your existing infrastructure.

The second section of this book will show you a variety of approaches to upgrading

[^hadoopRelease]: <http://hadoop.apache.org/releases.html#27+December%2C+2011%3A+release+1.0.0+available>
[^cassandraRelease]: Although Cassandra was available as early as 2008, it graduated to an Apache Top Level project in 2010 with version 0.6
