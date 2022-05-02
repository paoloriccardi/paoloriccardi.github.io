---
title: My implementation of the Dijkstra Algorithm, part 2
layout: post
categories: Data_Structures Algorithms
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: After covering the basics and definyng the class to represent the Graph that will be used by the Dijkstra Algorithm, which is illustrated in detail here in this article.
---

In the [first part]({% post_url 2021-04-30-dijkstra-algorithm-1 %}){:target="_blank"} of this article we covered the preliminary to present the Dijkstra Algorithm. 

We introduced the so called *greedy choice* or greedy *heuristic*, that brings the algorithm to make decisions based on local optimums, picking up the most promising alternative at every step. 

We also saw a way to represent an undirected, non-negatively weighted, Graph with some added functionalities that will be useful for the algorithm. 

Now we are ready to go... almost.

##### The Priority Queue

To get the most promising candidate at each step of the algorithm we use a priority queue, where the priority of each node is inversely related to the cost of reaching that node. 

The use of `heapq` allows a more efficient way of popping the element with lower cost compared to scanning the whole list of nodes looking for the one with the smaller cost. 
Why? Well, because `heapq` uses a data structure called heap, a tree structure that keeps the higher (or lower) priority element always in the root node, rebalancing the tree so that it complies with the "heap property" when nodes are popped or pushed into the structure.

By the way, creating our own priority queue using a heap data structure, instead of using `heapq` could be a good excuse to refresh heap's basics and that's another great benefit of learning this Algorithm, it's perfectly functional for a real life scenario (with some tweaks maybe) yet it relies on very basic concepts of DSA. 

##### The basic idea

In order to get the shortest paths in the Graph, the Algorithm "explores" the Graph, checking for the best opportunities that each node offers, up to the present moment, in terms of "neighborhood reachability". In the process of exploring each single node the algorithm makes a "greedy" choice in the sense that it chooses deliberately to "explore" first those candidates that looks more promising, regardless the fact that some steps later those promises may result less appealing. 

If and when better options will rise the algorithm will take them into account.
This is a very important consideration, because for practical applications, such as satellite navigation, instead of going fully breadth-first in our exploration we may want to somehow have a direction... for example, if you want to go from Florence (Center of Italy) to Milan (North of Italy), it's very unlikely although not impossible, that a shortest path may include Naples (South of Italy).


##### How the Algorithm works

A brief description of the code:
0. When the Dijkstra class is instantiated, for every node in the Graph, the constructor creates a dictionary called `distance`, where:
    - the keys are the nodes of the Graph;
    - the values are lists made of two elements, `[actual cost to reach the node from start, previous node in the actual minimum path]`, the second element is often called the *coming from* node or *prev* node;
    - for every node the values are initialized respectively to a proxy for infinity (a very big int) and to None, this means that at the first step of the algorithm every new path to the node will be considered an improvement;
1. When the algorithm is called we do the following with the starting node:
    - the initial value for the starting node in the distances is modified, the cost is set to *0* and the *coming from* to the node itself;
    - the starting node is added to the priority queue and the loop begin;
    - a list with the visited node is initialized
2. While there is still available candidates in the priority queue, the algorithm:
    - pops the node reachable with the smaller cost
    - retrieves the list of neighbors for the node (the adjacent nodes)
    - add the node to the visited list
    - the node is considered to be the actual node (the node we are ideally exploring)
3. The list of the neighbors is parsed and for each not-yet-visited node coming from it:
    - we retrieve the current cost for reaching the neighbor node checking the `distance` dictionary
    - we calculate the cost of reaching the actual node
    - if the cost of reaching the neighbor node passing from the actual node is smaller (or equal) than the old cost we had to pay to reach the node so far we update the `distance` dictionary with the new cost, setting the value for the *node from* to the actual node. _In other words we've found a better option to reach the neighbor node, so we will make use of it from now on_.
4. If the node is already in the queue we update its cost/priority value and re-heapify the priority queue itself, otherwise we just push the node to the queue using its cost as priority
5. When there is no more element in the priority queue, we return the dictionary of the distances which will contain the minimum cost to reach every node of the Graph, plus the last node visited in the shortest path for each node.


```python
import sys
import heapq

class Dijkstra:
    def __init__(self,aGraph):
        self.aGraph = aGraph
        self.distances = {}
        for node in aGraph.nodes:
            self.distances[node] = [sys.maxsize,None]

    def shortestPath(self,start):
        if start not in self.distances.keys():
            return
        self.distances[start] = [0,None]

        #first element of the tuple is used as priority
        priorityQ = [(0,start)]
        visited = []

        while len(priorityQ) > 0:
            _ , actual = heapq.heappop(priorityQ)
            neighbors = self.aGraph.neighbors[actual]
            visited = visited + [actual]
            for node in neighbors:
                if node not in visited:
                    dist_node , _ = self.distances[node]
                    dist_actual , _ = self.distances[actual]
                    if dist_node >= dist_actual + self.aGraph.weight(actual,node):
                        newdistance = dist_actual + self.aGraph.weight(actual,node)
                        self.distances[node] = [newdistance,actual] 

                        # whether the node was already in the priority queue or not we need to update 
                        # its value or to insert a new one
                        alreadyInPQ = False
                        for i in range(len(priorityQ)):
                            _ , pq_node = priorityQ[i]
                            if node == pq_node:
                                priorityQ[i] = (newdistance,node)
                                heapq.heapify(priorityQ)
                                alreadyInPQ = True
                                break
                        if not alreadyInPQ:
                            heapq.heappush(priorityQ,(newdistance,node))
                        
        return self.distances
```

