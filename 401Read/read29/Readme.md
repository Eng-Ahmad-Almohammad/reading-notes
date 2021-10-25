# Table of contents

|Read No. | Name of chapter|
|:---------: |:--------------:|
|29|[Graphs](Graphs.md)








# Graphs
### A graph is a non-linear data structure that can be looked at as a collection of vertices (or nodes) potentially connected by line segments named edges.
### Here is some common terminology used when working with Graphs:
1- Vertex - A vertex, also called a “node”, is a data object that can have zero or more adjacent vertices.
2- Edge - An edge is a connection between two nodes.
Neighbor - The neighbors of a node are its adjacent nodes, i.e., are connected via an edge.
3- Degree - The degree of a vertex is the number of edges connected to that vertex.


## Directed vs Undirected
### **Undirected Graphs**
### An Undirected Graph is a graph where each edge is undirected or bi-directional. This means that the undirected graph does not move in any direction.
### **Directed Graphs (Digraph)**
### A Directed Graph also called a Digraph is a graph where every edge is directed.

### Unlike an undirected graph, a Digraph has direction. Each node is directed at another node with a specific requirement of what node should be referenced next.
## Complete vs Connected vs Disconnected
### **Complete Graphs
### A complete graph is when all nodes are connected to all other nodes.
### **Connected
### A connected graph is graph that has all of vertices/nodes have at least one edge.

### **Disconnected
### A disconnected graph is a graph where some vertices may not have edges.
## Acyclic vs Cyclic
### **Acyclic Graph
### An acyclic graph is a directed graph without cycles. A cycle is when a node can be traversed through and potentially end up back at itself.
### **Cyclic Graphs
### A Cyclic graph is a graph that has cycles. A cycle is defined as a path of a positive length that starts and ends at the same vertex.
## Graph Representation:
## Adjacency Matrix
### An Adjacency matrix is represented through a 2-dimensional array. If there are n vertices, then we are looking at an n x n Boolean matrix

### Each Row and column represents each vertex of the data structure. The elements of both the column and the row must add up to 1 if there is an edge that connects the two, or zero if there isn’t a connection.
### a sparse graph is when there are very few connections. a dense graph is when there are many connections
## Adjacency List
### An adjacency list is the most common way to represent graphs. An adjacency list is a collection of linked lists or array that lists all of the other vertices that are connected.

### Adjacency lists make it easy to view if one vertices connects to another.
## Weighted Graphs
### A weighted graph is a graph with numbers assigned to its edges. These numbers are called weights.
### When representing a weighted graph in a matrix, you set the element in the 2D array to represent the actual weight between the two paths. If there is not a connection between the two vertices, you can put a 0, although it is known for some people to put the infinity sign instead.
### Within adjacency lists, you must include both the weight and the name of the adjacent vertex.
## Traversals
### ou will be required to traverse through a graph. The traversals itself are like those of trees. 
## Breadth First
### In a breadth first traversal, you are starting at a specific vertex/node. This node must be specified when calling the BreadthFirst() method. The breadth-first traversal of a graph is like that of a tree, with the exception that graphs can have cycles. When a graph has cycles and we are trying to traverse, this leaves the possibility to be in an infinite loop….this is bad. To prevent such behavior, we need to have some sort of flag that specifies if we have already visited that vertices. Upon each visit, we just set the “visited” flag from false to true.
### ere is what the algorithm breadth first traversal looks like:

1- Enqueue the declared start node into the Queue.
2- Create a loop that will run while the node still has nodes present.
3- Dequeue the first node from the queue
4- if the Dequeue‘d node has unvisited child nodes, mark the unvisited children as visited and re-insert them back into the queue.

## Depth First
### In a depth first traversal, we approach it a bit different than the way we do when working with a depth first traversal of a tree. Similar to how the breadth-first uses a queue, we are going to use a Stack for our depth-first traversal.

### The algorithm for a depth first traversal is as follows:

1- Push the root node into the stack
2- Start a while loop while the stack is not empty
3- Peek at the top node in the stack
4- If the top node has unvisited children, mark the top node as visited, and then Push any unvisited children back into the stack.
5- If the top node does not have any unvisited children, Pop that node off the stack
6- repeat until the stack is empty.
## Real World Uses of Graphs
### Graphs are extremely popular when it comes to it’s uses. Here are just a few examples of graphs in use:

- GPS and Mapping
- Driving Directions
- Social Networks
- Airline Traffic
- Netflix uses graphs for suggestions of products