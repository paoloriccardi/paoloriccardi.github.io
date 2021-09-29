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
The paper was so influential that its principles inspired noSQL databases like [Apache Cassandra](https://cassandra.apache.org/_/index.html){:target="_blank"}, [Riak](https://riak.com/){:target="_blank"} and, as the name may imply, [DynamoDB](https://aws.amazon.com/it/dynamodb/){:target="_blank"}.

The authors are basically the engineers behind the Amazon Dynamo database, a noSQL data store that was built in house to power many of the company's business critical services like the ecommerce shopping cart.
Given the nature of the service provided, Dynamo was designed to be *always on*, which translates to a high emphasis on availability. 

The reliability and scalability of a system is often dependent on the way its application state is persisted. Relational databases were and still are the one stop shop for pretty much everything, but usually the usage pattern for state persistence is just to store and retrieve data by primary key, without complex queries that rely on articulated relations between entities. In other words in such a scenario, using a RDBMS will mean paying for lots of extra benefits that you won't use. That's why for Dynamo a simple key-value approach was chosen.

Here's the assumptions that were made and the requirements that led the design of Dynamo as described in the paper:
- *Query Model -* read/write on data items uniquely identified by a key, no relational schema required and no operation can involve more than one data item
- *ACID properties -* Dynamo will choose Availability over Consistency any day of the week 
- *Efficiency -* The system will work on commodity hardware and will satisfy SLAs such as very low latency
- *Non-hostile environment -* Dynamo will be used just by internal services 

##### Availability vs Consistency
>Spoiler: *(in the paper) availability wins*.

The [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem){:target="_blank"} is a very simplistic result in distributed systems, but although its practical utility is questionable it is still a good starting point to understand the tradeoff between availability and consistency. The theorem states that in a distributed system where partitions (communication failures between nodes or groups of nodes) may occur you can only choose one between Availability and *(strong)* Consistency.

Roughly speaking, a service is Available when it provides meaningful responses to client requests. *Strong* Consistency is a more subtle concept but for now we can say that, from the client perspective, a consistent system behaves like a single node system. In other words, the client can assume that all the operations on the system happen as a linear sequence of actions, so if we read a data from two different nodes at the same time we should get the same value, just like there was a unique copy of that data in the system, that's why Consistency is often called *Linearizability*.

In real world scenarios the Consistency requirement is usually *relaxed* to a more easy going version, that's why the adjective *strong* is used to specify how much you wish to tolerate in terms of non-consistent states. 

For example, in a simple distributed system of two database replicas, `A` and `B`, when the link between them dies, they can choose to guarantee availability continuing to accept read/write from clients and eventually reconciling their state later, or they can decide to guarantee *Strong* Consistency, denying client requests in order to keep their state aligned, until the network link comes back to life.

To guarantee *strong* Consistency, a synchronous replication strategy between nodes can be enforced and this usually means some sort of price to pay in terms of Availability, which is something that the paper authors didn't want to happen, ever. 
Just to be sure that we are on the same page, the purpose of Dynamo is to accept requests from clients hence the system design has to maximize availability. To do so it's necessary to gracefully tolerate temporary node disconnections, propagating the updates in the background asynchronously and reconciling the state of the nodes later.

The Dynamo approach is based on the idea of *eventual* Consistency, which means that in case of partitioning, the nodes will keep serving requests, resolving conflicts later. So conflicts are temporary and eventually nodes will come to an agreement but of course until they do, they will have to decide:
- *when* to perform the process of resolving update conflicts (e.g. during reads or writes? Dynamo chooses to always accept writes and to resolve conflicts during reads)
- *who* performs the process of conflict resolution (e.g. the data store or the application? the first choice allows simplistic reconciliations like *Last Write Wins*, while the application can usually  make more sensible choices based on the user's needs)

Other key principles followed (or we should say proposed) by Dynamo are:
- Scale incrementally one node at a time
- Every node must have the same responsibilities
- Decentralized peer-to-peer system
- The system needs to distribute work proportionally to the capability of the nodes (to favour heterogeneity of hardware setups)

##### System Interface
Dynamo's interface exposes two operations: 
- `get(key)` locates the object replicas associated with the `key` in the storage system and returns a single objects (or a list of objects with conflicting versions) along with a *context* 
- `put(key, context, object)` determines where the replicas of the object should be placed based on its `key` and persist the replicas, `context` encodes system metadata about the object (e.g. its version). 

An hash of `key` is calculated to determine the storage nodes that will be responsible for storing/serving the key.

##### Partitioning
When we say that we want the system to scale incrementally, we're basically requiring a mechanism to dynamically partition the data (key-values) over a set of nodes that may change and that we would like a smooth process to allow a new node to join the party. This is done via [consistent hashing](https://www.cs.princeton.edu/courses/archive/fall09/cos518/papers/chash.pdf){:target="_blank"}.

The output from the hash function used (MD5) is a 128-bit number and in *consistent hashing* it's treated as a circular space, which means that the immediate follower of the max value that the hash can generate is the smallest one.

Each node in the system is associated with a random value by the hash function that will determine where the node will stand on the ring. The same is done for a key and once we've placed it according to its value we start walking the ring clockwise to find the first node which has a position larger than the key. This way, every node is responsible for the region of the ring between itself and its predecessor on the ring. Any departure or arrival of a node only affects its immediate neighbors while other nodes remain unaffected.

##### Replication
When you store your data in a system you don't want it to disappear on the other hand you want it to be there for you when you need it, which means that the data must be both available and durable. 

Replicating your data through multiple nodes is a common solution to mitigate the outcomes of node failures and to provide a more scalable solution to serve client requests. This often translates into better availability, even though going multi-node usually brings in concurrency issues, like the aforementioned consistency.

So each data is replicated and lives on different nodes (how many nodes is a parameter that can be configured). A *key* is assigned to a coordinator node which is in charge of the replication of the data items placed in his competence area on the ring of values given by the consistent hashing.
A *key* is then copied by the coordinator node  on a given number of nodes that are placed next to the coordinator on the hash ring (in clockwise order). Each node will hold the values for a given number of keys that he's responsible for and for a given number of keys replicated from other responsible nodes.

The list of nodes in charge of storing each key is called the *preference list*, so that even if a node fails there are others to cover for specific keys.

##### Example: simple consistent hash with replication
For instance, let's assume we have two keys, `k1` and `k2` and the nodes `A`, `B`,`C`,`D`,`E`. 
Our hash function returns values in the range of `{0,...,h_MAX-1}` and that the hash of both nodes and keys can be labeled as `h_k1`, `h_A`, etc...

Let's suppose that the hash value for key *k1* is `h_k1`, we start at this position on the ring and the next hash value of a node that we find walking the ring clockwise is `h_A`. So `A` will be the node responsible for storing `k1`. We can now decide to replicate the data on other nodes to increase durability and availability. For the sake of the example one replica is enough, so the key `k1` is copied to the node that follows  `A` on the ring, which is `B`. 

Same thing happens if we want to store `k2`, the first node that we find on the ring is `C` and the following which will keep its replica, is node `D`. 

Please note that in the drawing the node `A` is responsible for all the keys which have hash values smaller than `0` and greater than `h_E`.


We are now sure that any issue with one of the nodes will affect only its neighbours and furthermore we now have a way to determine which nodes are responsible for storing a certain key and where each and every replica belongs.

![consistent hashing](/images/consistent_hash.jpg){:width="75%" height="75%"}

To clarify further:
- Node `A` is responsible for the keys with hash value between `h_E` and `h_A`
- Node `B` is responsible for the keys with hash value between `h_A` and `h_B`
- Node `C` is responsible for the keys with hash value between `h_B` and `h_C`
- Node `D` is responsible for the keys with hash value between `h_C` and `h_D`
- Node `E` is responsible for the keys with hash value between `h_D` and `h_E`

Furthermore, in this particular example a replica for every key in a node is kept on the next following node on the ring, which is `B` for `A`, `C` for `B` and so on. To wrap everything up, `B` will contain all the keys with hash value between `h_A` and `h_B` *and* all the keys with hash value between `h_E` and `h_A`, this is true for every node.

This is a very simplistic model, because it doesn't take into account, for example, that two adjacent nodes may be physically hosted on the same server which would not be great if we want to tolerate server faults.
Furthermore different values for a key can occur, so we will need to find an agreement mechanism, like quorum for read/write operations and so on.

##### Versioning
As we mentioned in the example, one thing that could happen if you propagate changes on data asynchronously is that you will end up with inconsistent states, which means you could have a key that could have different versions of that same `key:value` at the same moment. 

Each different version of the data may live its own life span until they are reconciled one way or another (by the client application or by the nodes in the system).
The history deriving from each version may imply a causality chain between versions and subversions, to capture this dynamics, Dynamo uses [vector clocks](https://en.wikipedia.org/wiki/Vector_clock){:target="blank"}. 

To be (a little bit) more specific, in Dynamo a client that wants to update an object, it needs to specify which version is receiving the update, this information is provided by the client in the aforementioned *context*.

For further readings about ordering of events in distributed systems, I would recommend *Time, Clocks and the ordering of events in a Distributed System* by *Leslie Lamport*. You can find a copy of this paper [here](https://lamport.azurewebsites.net/pubs/time-clocks.pdf){:target="_blank"}.

##### First part conclusions
I found about this paper in the bibliography of the amazing [book](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/){:target="_blank"} *Designing Data-Intensive Applications*  by Martin Kleppmann. 
The book itself is a great reference and an interesting reading if you want to know more about distributed systems in theory and practice and it has inspired me up to a point that I had to start a [pet project](https://github.com/paoloriccardi/key-value-log){:target="_blank"} to get my fingers dirty with its contents. For those interested, the pet project is fundamentally a key value distributed datastore, but this will hopefully be covered by another post.

One of the first things that I've noticed, while reading the paper for the first time, is that it's dense. What's addressed in a couple of semicolons can easily take pages and pages on an average undergraduate course handbook about concurrency and distributed systems. 

The paper doesn't go very deep on every topic, it just gives you the general approach used to target each issue, like replication, versioning or handling failures.

I may be a little bit biased here, since a big piece of both my BS and MS course in Computer Science was about distributed systems and as such I was already both familiar with and interested in concurrency related problems but nonetheless I found the paper very insightful, everything was laid out in a straight line, with a very practical approach that has the merit to underline business outcomes for system design choices.


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
