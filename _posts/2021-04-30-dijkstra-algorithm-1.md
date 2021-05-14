---
title: My implementation of the Dijkstra Algorithm, part 1
layout: post
categories: DSA
permalink: /Linenoise/:categories/:title/
description: Dijkstra Algorithm is maybe the most famous algorithm in the domain of graph theory, it's a classic and for very good reasons. In the first part of the article we're going to cover the basics, defining a basic implementation of the Graph class that we're going to use in the second part.
---

In the last weeks I've tried to refresh some Data Structure and Algorithms (DSA) related concepts. Computer Science is a topic that can evolve pretty fast, it literally consumes buzzwords down to ashes, but the foundamentals always remain. 

This is still holds, despite the fact that you may spend years without the actual need to code a sorting algorithm from scratch, classics data structures and algorithms (DSA) are a unique way to keep your problem solving mind sharp. 
People that go running don't always do that because they run in their daily life, they do it because it makes them feel better, healtier and stronger. In my opinion it works the same way with computer science fundamentals.

Somebody may still argue that knowing how mergesort works is pointless, because you can just use the libraries included with your programming language of choice and live happily, well I have some bad news for those guys:
- I've seen firsthand the interviewing process in some big tech companies and they want your DSA to be as sharp as possible, so if you're considering applying for that software engineer role in Dublin for that big company, well... you cannot say I didn't warn you;
- Problem solving is maybe one of the most abused buzzword in every job position and conversely on every CV in tech, well in IT there's no solution without automation, and automation requires the ability to put an algorithm down right;
- If as a programmer, you reduce yourself to just use libraries and frameworks, you're going to be in big trouble when those libraries and those frameworks become deprecated or disappear from the scene;
- Finding your way around problems requires the ability to abstract, to grab the problem, wrap your head around it and reformulate it in an equivalent yet maybe more convenient way. This is a key point to deal with every situation that doesn't play by the book, imho;
- Never underestimate the value of training, try to run 10 km after 1 year of lockdown and you'll know what I mean.

##### What's Dijkstra Algorithm

Quoting The Algorithm Design Manual, by Steve Skiena: 

> Dijkstra’s algorithm is the method of choice for finding shortest paths in an edge and/or vertex-weighted graph. Given a particular start vertex **s**, it finds the shortest
path from **s** to every other vertex in the graph, including your desired destination
**t**. 

The algorithm finds the shortest path between two nodes in a weighted Graph with no negative weights on the edges. Every edge contribute to the "cost" of the path with its weight, Dijkstra Algorithm guarantees to find the path with the lower cost.

The algorithm was [published](http://www-m3.ma.tum.de/foswiki/pub/MN0506/WebHome/dijkstra.pdf){:target="_blank"} in the 50's and it's still widely studied and used in computer science as well as in real world applications, like satellite navigation or video games.

The algorithm starts in a given starting node, it looks around looking for the nodes connected to the actual node and it evaluates the cost for reaching them from the starting node (either directly or not). The algorithm now applies a so called *greedy* choice, which means it makes the picks that looks more promising in that very moment. 

To do so it moves to the node which is reachable with lower cost from the starting node. Once in the new node, again, it looks around looking for newly connected nodes noting the cost for reaching them from the starting node (or updating its cost, if a new more promising path arises).

##### Is Dijkstra Algorithm Greedy?

If you google the question you'll find out that it is  a debated topic. My 2 cents is that it depends a lot on the perspective under which it is defined and presented. 

As we will see better in the [second part]({% post_url 2021-05-01-dijkstra-algorithm-2 %}){:target="_blank"}  of this article, the Dijkstra Algorithm decides which node to *explore* first based on which one is reachable (or rather connectable to the minimum spanning tree) at the lower cost.

This is definitely a *greedy* heuristic, because it chooses a locally optimal alternative at each stage. Furthermore, the choice is never reverted, because an *explored* node goes straight into the minimum spanning tree.

Does that means that the algorithm cannot be presented as a dynamic programming problem? Absolutely not.
The fact that the shortest path *P* between two nodes will contain other shortest paths between the node traversed in *P* it's called *optimal-substructure*, which indeed opens up to both dynamic programming and greedy approaches.

If you're curious you can check a dynamic programming approach [in this paper](http://matwbn.icm.edu.pl/ksiazki/cc/cc35/cc3536.pdf){:target="_blank"}.


##### The Graph

Dijkstra algorithm works on weighted Graph with positive weight on the edges.
So we will need a way to represent a Graph and to support useful functions, like getting the list of neighbors of a given node or the weight of a given edge.

In discrete mathematics a Graph *G* is simply a pair *G = (V,E)* where *V* is the set of Vertex (nodes) and *E* is a set of paired vertices, whose elements are called edges.

Graphs are so useful because they can represent basically *any* relationship or set of relationships. For example, I've used graphs quite a lot in *Process Mining* to represent the *Social Network*, which is the networks that maps the handover of work inside of a business process. More on that, a Business Process is: "A set of structured activities that produce value to the customer", well that structure is made of workflows of business activities and it is actually modeled quite well as a graph.

Back to Computer Science world, the discrete mathematics definition still works quite well, we only have to keep in mind that we will need each edge to be weighted. In practice smart(er) ways are used in order to represent a Graph on a computer, for example adjacency matrix adjacency lists.

Adjacency lists is the most common way to represent a Graph and it consists basically in keeping, for every node, a list of its neighbors (the so called adjacent nodes, hence the name).

For the Dijkstra Algorithm we will need to keep an adjacency list for each node in the Graph and we will need a method to return the weight for an edge connecting two nodes.
In my implementation for the Graph, an edge is a tuple consisting of `(source_node, destination_node, weight)`.



```python


#Undirected Graph
class Graph:
    def __init__(self,E):
        self.edges = E
        self.neighbors = self.__neighborList(self.edges)
        self.nodes = self.neighbors.keys()

    #private function to generate the neighbors for every node of the Graph
    def __neighborList(self,edges):
        neighbors = {}
        #an edge is a list made of [source, destination, weight]
        for edge in edges:
            source_node, dest_node, _ = edge
            if source_node in neighbors.keys():
                neighbors[source_node] = neighbors[source_node] + [dest_node]
            else:
                neighbors[source_node] = [dest_node]
            if dest_node in neighbors.keys():
                neighbors[dest_node] = neighbors[dest_node] + [source_node]
            else:
                neighbors[dest_node] = [source_node]
        return neighbors

    def weight(self,node_a,node_b):
        if node_a not in self.neighbors[node_b]:
            return None
        for edge in self.edges:
            src, dst, weight = edge
            # direction in edges doesn't matter
            if (node_a == src or node_a == dst) and (node_b == src or node_b == dst) :
                return weight

```

Continue to the [second part]({% post_url 2021-05-01-dijkstra-algorithm-2 %}){:target="_blank"}