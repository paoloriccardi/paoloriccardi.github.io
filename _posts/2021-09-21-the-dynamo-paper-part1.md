---
title: The Dynamo paper, part 1
layout: post
categories: DS
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: The famous Dynamo paper is, well... a paper published in 2007 by the group of Amazon engineers. It describes in just 16 pages, including a rich bibliography, an highly available (distributed) key-value store which became DynamoDB and eventually inspired many others noSQL databases like Cassandra and Riak. It's considered by many one of the most influential papers ever written on databases. To me it was mind blowing and I strongly recommend it to anyone who's even remotely interested in distributed systems, noSQL and databases in general.
---

##### Introduction
Let's start from the beginning, the original title was *"Dynamo: Amazon Highly Available Key-value Store"*, it was published in 2007 and you can download it [here](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf){:target="_blank"}. 

The paper was so influential that its principles inspired noSQL databases like [Apache Cassandra](https://cassandra.apache.org/_/index.html){:target="_blank"}, [Riak](https://riak.com/){:target="_blank"} and (needless to say) [DynamoDB](https://aws.amazon.com/it/dynamodb/){:target="_blank"}.

The authors are basically the engineers behind the Amazon Dynamo database, a noSQL data store built in house to power many of their business critical services like the ecommerce shopping cart.
Given the nature of the service provided, Dynamo was designed to be *always on*, which translates into a high emphasys on availability. 

The reliability and scalability of a system is often dependent on the way its application state is persisted. Relational databases were and still are the one stop shop for pretty much everything, but usually the usage pattern for state persistence is just to store and retrieve data by primary key, without complex relational queries. In other words in such a scenario, using a RDBMS will mean paying for extra benefits that you won't use. That's why for Dynamo a simple key-value approach was chosen.

Here's the assumptions and the requirements that led the design of Dynamo as described in the paper:
- *Query Model* read/write on data items uniquely identified by a key, no relational schema required and no operation can involve more than one data item
- *ACID properties* Dynamo will choose Availability over Consistency any day of the week 
- *Efficiency* The system will work on commodity hardware and will satisfy SLAs such as very low latency
- *Non-hostile environment* Dynamo will be used just by internal services 

##### Availability vs Consistency
>Spoiler: *in the paper availability wins*.

The [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem){:target="_blank"} is a very simplistic result in distributed systems, but although its practical utility is questionable it is still a good starting point. The theorem states that in a distributed system where partitions (communication failures between nodes or groups of nodes) may occur you can only choose one between Availability and *strong* Consistency.

Roughly speaking, a service is Available when it provides meaningful responses to clients. *Strong* Consistency is a more subtle concept, a consistent system behaves like there's always a single version of the data.
In real world problems the Consistency requirement is usually *relaxed* to a more easy going version, that's why I've used the adjective *strong*. 

An alternate formulation of Consistency is Linearizability.
A system is Linearizable if a set of requests that can be considered as a linear sequence of actions, which means that from the client point of view, she's dealing with a single node system.

For example, in a simple distributed system of two database nodes, `A` and `B`, when the link between them dies, the nodes can choose to guarantee availability continuing to accept read/write and eventually reconciling their state later, or they can guarantee *Strong* Consistency, denying client requests in order to keep their state aligned, until the network link comes back to life.

To guarantee *strong* Consistency a synchronous replication strategy between nodes can be enforced and this usually means some kind of tradeoff on Availability, which is something that the paper authors didn't want to happen. 
What they wanted instead was to maximize availability and to do so they needed to tolerate temporary nodes disconnection, propagating the updates in the background asynchronously and reconciling the state of the nodes later.

In other words, they embraced the concept of *eventual* Consistency, which means that in case of a partition, the nodes will keep serving requests, resolving conflicts in their states later. This means that conflicts are temporary and that nodes will come to an agreement, but in the meantime they need to decide:
- *when* to perform the process of resolving update conficts (e.g. during reads or writes? Dynamo chooses to always accept writes and to resolve conflicts during reads)
- *who* performs the process of conflict resolution (e.g. the data store or the application? the first choice allows simplistic reconciliations like *Last Write Wins*, while the application can usually  make more sensible choices based on the user's needs)

Other key principles followed (or we should say proposed) by Dynamo are:
- Scale incrementally one node at a time
- Every node must have the same responsibilities
- Decentralized peer-to-peer system
- The system needs to distribute work proportionally to the capability of the nodes (to favour heterogeneity of hardware setups)

##### Architecture

##### System Interface
Dynamo's interface exposes two operations: 
- `get(key)` locates the object replicas associated with the `key` in the storage system and returns a single objects (or a list of objects with conflicging versions) along with a *context* 
- `put(key, context, object)` determines where the replicas of the object should be placed based on its `key` and persist the replicas, `context` encodes system metadata about the object (e.g. its version). 

An hash of `key` is calculated to determine the storage nodes that will be responsible for storing/serving the key.

##### Partitioning
When we say that we want the system to scale incrementally, we're basically requiring a mechanism to dynamically partition the data (key-values) over a set of node that may change, this is done via [consistent hashing](https://www.cs.princeton.edu/courses/archive/fall09/cos518/papers/chash.pdf){:target="_blank"}.

The output from the hash function used (MD5) is a 128-bit number and in *consistent hashing* it's treated as a circular space, which means that the immediate follower of the max value that the hash can generate is the smallest one.

To each node in the system is associated a random value by the hash function, that is to say a position on the ring. The same is done for a key and once we've placed it according to its value we start walking the ring clockwise to find the first node which has a position larger than the key. This way, every node is responsible for the region of the ring between itself and its predecessor on the ring. Any departure or arrival of a node only affects its immediate neighbors while other nodes remain unaffected.



##### Replication

##### Versioning


##### First part conclusions
I found about this paper in the bibliography of the amazing [book](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/){:target="_blank"} *Designing Data-Intensive Applications*  by Martin Kleppmann. I hope I will be able to write some posts on that book too because it contains a lot of interesting stuff about distributed systems and because it pushed me to start a [pet project](https://github.com/paoloriccardi/key-value-log){:target="_blank"} which is fundamentally a key value distributed datastore, but this too will hopefully be covered in another post.

One of the first thing that I've noticed, while reading the paper for the first time is that it's dense of concepts, what's addressed in a couple of semicolons can easily take pages and pages on an average undergraduate course handbook about concurrency. 

Indeed, a big piece of both my BS and MS course in Computer Science was about distributed systems, so I was already familiar with concurrency related problems and topics in general, yet I found the paper very insightful, everything was laid out in a straight line, with a very practical approach.

Of course the paper doesn't contain a full discussion on topics like replication, partitioning etc... it just defines the problems they wanted to address and explains a possible solution. If you want to go deep about these topics, then the Martin Kleppmann book linked above is a great resource.

<!---
##### Table of contents
- Introduction
    - System assumption and requirements
    - Design considerations
- Related Work
    - p2p
    - Distributed  filesystems / databases
- Architecture
    - Interface
    - Partitioning algorithm
    - Replication
    - Versioning
    - Execution (get/put)
    - Handling failures
    - Add/remove nodes
- Implementation
- Lessons learned
    - Balancing performance and durability
    - Load distribution
    - Divergent versions
    - Client driven / server driven coordination
    - Balancing BG and FG tasks
- Bibliography
-->
