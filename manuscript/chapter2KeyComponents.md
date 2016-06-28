# Starting Grid

Every system is going to be comprised of a number of different components. For
a large data system, these tend to fall into five main categories, with each
category having a distinct set packages / underlying pieces of technology.

Sometimes these components are tightly coupled, but more often than not are
frequently loosely coupled.  This has several advantages.  First, by loosely
coupling the various components you give yourself the option of independently
upgrading the individual pieces of your infrastructure without changing out
the other components.

Second, through loose coupling there is a greater opportunity to build in
redundancy, improving your ability to deal with a failure of an individual set of
components without adversely affecting your entire ecosystem any time there is
an individual component, part of your pipeline, or server crashing and burning.

## Some things are universal

### Primary data storage

One common element of nearly every infrastructure is a back end data store.  Today
there are a plethora of options available, and it is increasingly likely that there
is more than one data store at play, with hybrid SQL and NoSQL storage solutions
becoming more commonplace.  (I am a proponent of hybrid solutions because of the
wide variance of use cases in a large product).

### Events

Events represent the individual blocks of data that your entire system is built
to store, analyze, and deliver to your customers.  By considering any incoming
data as an event, it becomes simpler to describe approaches to storing this data
in scalable, repeatable ways.  This is integral to simplifying your infrastructure
upgrade process and lets itself to the modularity that I mentioned in the introduction.

Events can be as simple as a single database update, i.e. changing an address.  They
can be as represent the output of a set of product recommendations that you want
to be able to recall at some point.  Events can range from log messages to machine
learning output to stream processing intermediate steps.

### Access

Data is no good if you've no method to get use it. It doesn't matter how many records
per second a data store can handle if there is no means to use that data in a
meaningful way.

There are a number of ways users will access your data, APIs, front ends, reports /
batch job output.

## Some things are just good ideas

### Queuing / Messaging systems

You've got events. You've got somewhere for them to ultimately live. But how do
they get from point A to point B. Using a solid messaging platform enables you to
to create an independent system to publish your data to; creating isolation
between your data store and anything that generates that data. Doing this gives
you a greater ability to change other components with a minimal amount of risks
involved.

There are a number of options in the marketplace for a solution like this. In my
opinion the best open source solution to this problem is Apache Kafka[^kafkaLink]
or the commercialized version available from Confluent[^confluentLink].  Kafka
provides a topic based queuing system that can support multiple consumers for
a single topic, partitioned data, guaranteed ordering, and a number of other
features that make it particularly well suited for modular and extendable systems.

There are also cloud based solutions available like Amazon's Kinesis[^kinesisLink].
Similar to Kafka, Kinesis allows for a topic based system with multiple consumers.
However, Kinesis is not nearly as configurable and has a number of limitations, such
as a very short term data retention policy.

One of the key components to consider when choosing some sort of queue/messaging
system is the data retention policy/policies that are available.  Depending on your
upgrade path you may need to be able to tweak how long data in the queue is retained
in order to facilitate a successful upgrade.  It is also very possible to need to
tune the retention policy to deal with excess data / running out of storage.

In general, using a scalable and well tested message queue provides a number
of benefits independent of upgradability of your stack.  Primarily it also provides
a central hub that is usually fairly scalable, both vertically and horizontally. This
also gives you the ability to scale individual components of your system independently.

For example, if you have a set of analytics based consumers that are very compute
intensive, you may need additional nodes to keep up with incoming traffic. If everything
is largely decoupled, then you would be able to spin up additional nodes independently
of your data producers or other data consumers.

### Analytics

Similar to general access to data, there isn't much use in storing a lot of information
in a 'big data' platform unless it is going to be analyzed.  Analytics mean a number
of things to various groups of people.  For data scientists it will often mean having
a simple means to access sample data sets to play with.  For a data or software engineer
it will often mean a platform to run map-reduce jobs, Spark, or something similar.  For
the C-Suite executive it means deriving the most important summary of information
to help them guide the business.

Regardless of the end result, there is often the need to have some sort of infrastructure
in place to support analytics.  This can, but does not need to be, tightly coupled
with your data storage solution.  Tighter coupling has some advantages such as data
locality, but also drawbacks, i.e. if you want to upgrade your analytics platform you
need to simultaneously upgrade your data store.

Similarly there are platforms that are tightly coupled with messaging systems.

[^kafkaLink]: <http://kafka.apache.org/documentation.htmlcon>
[^confluentLink]: <http://www.confluent.io/>
[^kinesisLink]: <https://aws.amazon.com/kinesis/>
