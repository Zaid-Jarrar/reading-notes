# Reading 35 - Graphs

## Graphs

**graphs** - non-linear data structure that can be looked at as a collection of vertices/nodes potentially connected by line segments named *edges*.

### Terminology

**vertex** - aka `node`. Data object that can have zero or more adjacent vertices.

**edge** - connection between two `nodes`.

**neighbor** - adjacent `nodes` of a node/connected via an *edge*.

**degree** - number of edges connected to that vertex.

### Directed vs Undirected 

**undirected graphs** - each edges is undirected or bi-directional (undirected graph does not move in any direction)

**directed graphs** (diagraphs) - graph where every edge is directed. Each node is directed at another node with a specific requirement of what `node` should be referenced next.

### Complete vs Connected vs Disconnected

Three types of graphs:

1.**Complete Graph** - all nodes are connected to all other nodes.

2.**Connected Graph** - has all of vertices/nodes have at least one edge.

3.**Disconnected** - some vertices may not have edges.

### Acyclic vs Cyclic

**Acyclic Graph** - directed graph w/o cycles.
-directed acyclic graph --> tree
-cycle - when a node can be traversed through and potentially end up back at itself.

**Cyclic Graph** - graph has cycles.
-cycle - path of a positive length that starts and ends @ the same vertex.

### Graph Representation

**Adjacency Matrix** - a way to represent a graph. If it is represented through 2 dimensional array. If n vertices --> nxn Boolean matrix.

-each row and column represents each vertex of the data structure.

-undirected graph will always be symmetric, but not a directed one.

-**sparse graph** - few connections

-**dense graph** - high connections

**Adjacency List** - collection of linked lists/array that lists all other vertices that are connected.
-easy to see if one vertices connects to another.

### Weighted Graphs

**weighted graph** - graph with numbers ("heights") assigned to its edges.

*note* in adjacency list- must include both weight and name of the adjacent vertex.
-to represent vertices weight, use key/value pair

### Traversals

-similar to trees

#### Breadth First

-start at specific vertex/node

1.Enqueue the declared start node into the `Queue`.

2.Add root to visited set, add children it hasn't visited yet to `queue`.

3.Dequeue first node from the queue

4.If the `Dequeue`'d node has unvisited child nodes, add the unvisitd children to visited set and insert them into the queue.

```python
ALGORITHM BreadthFirst(vertex)
    DECLARE nodes <-- new List()
    DECLARE breadth <-- new Queue()
    DECLARE visited <-- new Set()

    breadth.Enqueue(vertex)
    visited.Add(vertex)

    while (breadth is not empty)
        DECLARE front <-- breadth.Dequeue()
        nodes.Add(front)

        for each child in front.Children
            if(child is not visited)
                visited.Add(child)
                breadth.Enqueue(child)   

    return nodes;
```

#### Depth First

1.`Push` root node into the stack

2.Start a while loop while stack is not empty

3.`Peek` at top node in the stack

4.If top node has unvisited children, mark top node as visited, then `push` any unvisited children back to stack.

5.If top node doesn't have any unvisited children, `pop` that node off the stack.

6.Repeat until stack `isEmpty`.

