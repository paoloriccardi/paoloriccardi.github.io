---
title: The Dynamo paper, part 1
layout: post
categories: DS
permalink: /Linenoise/:categories/:title/
description: The famous Dynamo paper is, well... a paper published in 2007 by the group of Amazon engineers. It describes in just 16 pages, including a rich bibliography, an highly available (distributed) key-value store which became DynamoDB and eventually inspired many others noSQL databases like Cassandra and Riak. It's considered by many one of the most influential papers ever written on databases. To me it was mind blowing and I strongly recommend it to anyone who's even remotely interested in distributed systems, noSQL and databases in general.
---

##### Introduction
Let's start from the beginning, the article original title was *"Dynamo: Amazon Highly Available Key-value Store"*, it was published in 2007 and you can download it [here](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf){:target="_blank"}. 

The paper was so influential that its principles inspired noSQL databases like [Cassandra](https://cassandra.apache.org/_/index.html){:target="_blank"}, [Riak](https://riak.com/){:target="_blank"} and (needless to say) [DynamoDB](https://aws.amazon.com/it/dynamodb/){:target="_blank"}.

The authors are basically the engineers behind the Amazon Dynamo database, an noSQL data store built in house which, at the time, powered many company business critical services like the ecommerce shopping cart.
Powering such business critical features implied that Dynamo was designed to be *always on*, which translates into a high emphasys on availability.

The reliability and scalability of a system is often dependent on the way its applications state. Relational databases were and still are the main solution for pretty much everything but usually the usage pattern for service state persistence is just to store and retrieve data by primary key, without complex relational queries. In other words you're going to pay for the extra benefits of a RDBMS that you won't use. That's why for Dynamo was chosen a simple key-value approach.

To be more specific, here's the assumptions and the requirements that led the design of Dynamo as described in the paper:
- Query Model: read/write on data items uniquely identified by a key, no relational schema required and no operation can involve more than one data item
- ACID properties: Dynamo will choose Availability over Consistency any day of the week 
- Efficiency: The system will work on commodity hardware and will satisfy SLAs such as very low latency
- Non-hostile environment: Dynamo will be used just by internal services 

##### Design principles, the CAP theorem (again)

The [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem){:target="_blank"} is a very simplistic result in distributed systems, but although its practical utility is questionable it is always a good starting point. The theorem states that in a distributed system where partitions (communication failures between nodes or groups of nodes) may occur you can either choose one between Availability and *strong* Consistency.
In other words in a simple distributed system of two database nodes, A and B, when the link between them dies, the nodes can ignore the failure for the moment and keep serving read/write requests (eventually reconciling their state later, somehow) or they can deny the service to preserve the consistency of their state, until the link comes back to life.

In real world problems the Consistency requirement is *relaxed* to a more easy going version, that's why I'm using the adjective *strong* in the formulation of the theorem and it means that every client will have the same view on the data kept in the nodes in any given time. 

These kind of strongly consistent systems are also called Linearizable (and strong consistency is called Linearizability) because clients requests can be considered as a linear sequence of actions. Even though they happen in a concurrent system, a linearizability give clients the illusion to deal with a single node system.

To guarantee *strong* Consistency a synchronous replication strategy between nodes can be enforced and this usually mean some kind of tradeoff on Availability which again, is something that the authors didn't want to happen. 
What they wanted instead was to maximize availability and to do so they needed to tolerate temporary nodes disconnection, propagating the updates in the background asynchronously and reconciling the state of the nodes in a second time.

This last consideration lead to the necessity to decide:
- *when* to perform the process of resolving update conficts (e.g. during reads or writes? Dynamo chooses to always accept writes and to resolve conflicts during reads)
- *who* performs the process of conflict resolution (e.g. the data store or the application? the first one can typically allow simplistic reconciliations like LWW, while the application usually can make more sensible choices based on the user's needs )

Other key principles followed (or we should say proposed) by Dynamo are:
- Scale incrementally one node at a time
- Every node must have the same responsibility
- Decentralized peer-to-peer system
- The system needs to distribute work proportionally to the capability of the node (to favour heterogeneity of hardware)



##### Conclusions
I found about this paper reading the bibliography of the amazing [book](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/){:target="_blank"} *Designing Data-Intensive Applications*  by Martin Kleppmann. I hope I will be able to write some posts on that book too because it contains a lot of interesting stuff about distributed systems and because its reading pushed me to start a [pet project](https://github.com/paoloriccardi/key-value-log){:target="_blank"} which is fundamentally a key value distributed datastore, but this too will hopefully be the topic for another post.

A big piece of both my BS and MS course in Computer Science was about distributed systems, so I was already familiar with concurrency related problems in general, yet I found the paper very insightful, everything was laid out very logically and if you think about all these things condensed in just 16 pages you have to admit it was a pretty elegant synthesis too. 

Of course the paper doesn't contain a full discussion on topics like replication, partitioning etc... it just defines the problem and explain a possible solution. I would say that for a more deep treatment of those issues the Martin Kleppmann book linked above is a great resource.

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
