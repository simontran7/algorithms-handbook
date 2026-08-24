# Graph

## Theory
 
### Terminology

- **Graph $G$, vertices, and edges**: a pair $(V, E)$, where $V$ is a set of nodes, called **vertices**, and $E$ is a collection of pairs of vertices, called **edges**.
- **Directed Edge**: an ordered pair of vertices $(u, v)$, where $u$ is the origin, and $v$ is the destination.
- **Undirected Edge**: an unordered pair of vertices $(u, v)$.
- **Directed Graph (Digraph)**: a graph where all the edges are directed. 
- **Undirected Graph**: a graph where all the edges are undirected.
- **Endpoints of an edge $e$**: the end vertices of $e$.
- **Degree of a vertex $v$**: the total number of incident edges to $v$.
- **Incident edges of a vertex $v$**: all the edges that connect directly to that specific vertex.
- **Adjacent Vertices $v$, $w$**: two vertices $v$, $w$ are adjacent vertices if they are joined by the same direct edge.
- **Parallel Edges $e_1$, $e_2$**: two edges $e_1$, $e_2$ are parallel edges if they connect the *exact* same pair of vertices.
- **Self-loop**: an edge that connects a vertex directly to itself.
- **Path $(v_1, \dots, v_n)$**: a sequence of alternating vertices and edges, beginning with a vertex $$ and ending with a vertex $$.
- **Simple Path**: a path such that all its vertices and edges are distinct.
- **Cycle**: a circular sequence of alternating vertices and edges.
- **Simple Cycle**: a cycle such that all its vertices and edges are distinct (except for its first and last vertex).
- **Subgraph $S$ of a Graph $G$**: a graph such that the vertices of $S$ are a subset of the vertices of $G$, and the edges of $S$ are a subset of the edges of $G$
- **Spanning Subgraph of a Graph $G$**: a subgraph that contains all the vertices of $G$.
- **Connected Graph**: a graph where there is a path between every pair of vertices.
- **Connected component of a graph $G$**: a maximal connected subgraph of $G$.
- **Acyclic Graph**: a graph without any cycles.
- **Tree**: a connected, acyclic, undirected graph.
- **Forest**: a set of trees that are not necessarily connected between each other.
- **Spanning Tree of a Graph $G$**: a spanning subgraph of $G$ that is a tree.
- **Spanning Forest of a Graph $G$**: a spanning subgraph of $G$ that is a forest.
  
## Properties

- A complete graph has $\binom{V}{2} = \frac{V(V-1)}{2}$ edges
- A tree has $V-1$ edges
- A dense graph has $O(V^2)$ edges, while a sparse graph has $O(V)$ edges

## Interface

```
pub trait Graph {
    type Vertex;
    type Edge;

    /// Returns the number of vertices in the graph.
    func vertex_count(&self) -> UInt;

    /// Returns the number of edges in the graph.
    func edge_count(&self) -> UInt;

    /// Returns the edge from `u` to `v`, if one exists.
    func get_edge(&self, u: &Self::Vertex, v: &Self::Vertex) -> Option<&Self::Edge>;

    /// Returns the two endpoints of edge `e`.
    func endpoints(&self, e: &Self::Edge) -> (&Self::Vertex, &Self::Vertex);

    /// Returns the vertex opposite `v` on edge `e`.
    func opposite_vertex(&self, v: &Self::Vertex, e: &Self::Edge) -> &Self::Vertex;

    /// Returns the number of outgoing edges from `v`.
    func out_degree(&self, v: &Self::Vertex) -> UInt;

    /// Returns the number of incoming edges to `v`.
    func in_degree(&self, v: &Self::Vertex) -> UInt;

    /// Inserts a vertex storing element `x`.
    func add_vertex(&mut self, x: Self::Vertex);

    /// Inserts an edge `(u, v)` storing element `x`.
    func add_edge(&mut self, u: &Self::Vertex, v: &Self::Vertex, x: Self::Edge);

    /// Removes vertex `v` and all incident edges.
    func remove_vertex(&mut self, v: &Self::Vertex);

    /// Removes edge `e`.
    func remove_edge(&mut self, e: &Self::Edge);

    /// Returns all incoming edges to `v`.
    func incoming_edges(&self, v: &Self::Vertex) -> impl Iterator<Item = &Self::Edge>;

    /// Returns all outgoing edges from `v`.
    func outgoing_edges(&self, v: &Self::Vertex) -> impl Iterator<Item = &Self::Edge>;

    /// Returns all vertices in the graph.
    func vertices(&self) -> impl Iterator<Item = &Self::Edge>;

    /// Returns all edges in the graph.
    func edges(&self) -> impl Iterator<Item = &Self::Edge>;
}
```

## Adjacency List

```python
from collections import defaultdict

def from(edges):
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u) # comment out this line if the input is a directed graph

    return graph
```

```python
from collections import defaultdict

def from(adjacency_matrix):
    graph = defaultdict(list)
    n = len(adjacency_matrix)

    for i in range(n):
        for j in range(i + 1, n):
            if adjacency_matrix[i][j]:
                graph[i].append(j)
                graph[j].append(i) # comment out this line if the input is a directed graph

    return graph
```

## Adjacency Matrix
