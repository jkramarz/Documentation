# About Yothalot

Yothalot was built by Copernica BV in Amsterdam. We are a leading Dutch
provider of Email Marketing solutions, and we tried to setup a Hadoop
cluster to process our logs. However we like things to be simple,
and got annoyed by a number of things:

- The special-purpose HDFS file system
- The Java API (and lousy API's in other languages)
- The complexity and delay in running tasks
- Bad documentation and examples.


## What's wrong with HDFS?

Hadoop uses HDFS, which is a special-purpose distributed user space 
file system, which requires special tools and special (Java) libraries 
to read and write from files. There might be nothing wrong with this,
but we are mainly a C++ and PHP company, with a large code base 
in which we deal with files using calls like "fopen()", "fwrite()" and 
"fclose()" - and our operations department also prefers tools like "ls", 
"mkdir" and "less". Switching to HDFS would not make things easier.

We therefore decided not to use HDFS, but GlusterFS. This allowed us 
to use the functions and tools mentioned above, and still have a 
distributed file system for our map/reduce jobs.


## What's wrong with Java?

The second thing that annoyed us was the Java API. Hadoop is fully 
implemented in Java, with a Java API. There is, once again, in principe 
nothing wrong with Java, but Copernica is a non-Java organization. We 
just happen to have a team full of qualified and experienced PHP and 
C++ programmers, and most of our business logic is written in these 
languages as well.

If we had to write map/reduce algorithms in Java, many people from our
team would have to learn this new language, and we would be unable to 
use the functions and objects from our existing data models. That would 
be a waste.

We tried to use the other Hadoop API's, like the C++ API, but we
struggled to get it running, and to find our way through the sparse
documentation.


## Hadoop tasks startup time

When we finally had our first C++ map/reduce job running, we were 
surprised by the complexity of just deploying this single wordcount 
example. It was much more complicated than we thought was necessary, and
at the same time it took almost a minute before the task even started 
to run.

One could of course argue that Hadoop was not designed to run such 
small tasks, and the real gain comes when you start using it for really
big tasks, but in the end we were not impressed by the overhead of 
starting up that initial wordcount example.


## So we wrote Yothalot

All these frustrations, and the fact that the actual map/reduce 
algorithm did not look that complicated, led to the conclusion that we 
would be better off writing our own alternative map/reduce system. In 
the end it came just down to combining ingredients: we use GlusterFS for
the distributed file system, RabbitMQ for reliable communication between 
jobs and nodes, and PHP as the scripting language in which map/reduce
tasks can be written (you can use other languages too by publishing
jobs to RabbitMQ directly, but we already created an extensive PHP API).

Our Yothalot product turns out to be a powerful solution, that allows
one to write map/reduce algorithms in PHP to process huge log files (and
to process other kinds of data). The Yothalot master process splits up 
the tasks into smaller sub jobs and distributes these sub jobs over the 
servers in the cluster. By running al these jobs in parallel we manage 
to process huge sets of data.


## Yothalot was not built with PHP

Before you draw the conclusion that it is weird that Yothalot relies
so much on PHP, it may be nice to know that Yothalot itself is a C++ 
application. We use PHP for writing the actual map/reduce job, so that
even beginning programmers can write map/reduce jobs, but the Yothalot
core of the map/reduce algorithm has a native implementation, and is 
highly reliable. 