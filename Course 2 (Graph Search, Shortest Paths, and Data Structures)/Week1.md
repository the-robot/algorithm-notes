Week 1
---

**Breadth First Search**
- O(m+n)
```python
mark S as explored
let Q = queue data structure, initialized with S

while Q != empty:
  remove first node from Q, call it v
  
  for each edge (v, w):
    if w is unexplored:
      mark w as explored
      add w to at the end of Q
```
<br>

**Equivalence Relation**
1. Reflexive, everything has to be related to itself
2. Couple of relations have to be symmetric, if u and v are related, v and u are related
3. Transitive, u and v are related and so are v and w and u and w

> in undirected graphs, two vertices are connected if they have a path connecting them. How should we define connected ina directed graph?
> We say that a vertex a is strongly connected to b if there exist two paths, one from a to b and another from b to a.

<br>

**Depth First Search**
- also computes a topological ordering of a directed acyclic graph
- strongly connected components of directed graphs
- O(m+n)
```python
DFS(graph G, start vertex S):
  mark S explored
  for every edge (S, v):
    if v is unexplored:
      DFS(G, v)
```

<br>

**Topological Sort**
- sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering.
```python
DFS-Loop(graph G):
  mark all nodes unexplored
  current_label = n  # to keep track of ordering
  
  for each vertex v in G:
    if v is unexplored:
      DFS(G, v)

set f(s) = current_label
current_label-- 
```
<br>

**Kosaraju's Two-Pass Algorithm**
1. Let G$$^{rec}$$ = G with all arcs reversed
2. run DFS-Loop on G$$^{rev}$$  (to compute *magical ordering* of nodes)
3. run DFS-Loop on G  (to discover the SCC one-by-one)

> **Procedure**  
> 1. G is a directed graph and S is a stack.
> 2. while S does not contain all vertices perform step 3.
> 3. choose a random vertex v and perform Depth First Search on it. Each time DFS finishes expanding vertex v, push v on the stack S (This gurantees that the vertex with maximum finish time will more closer to the top of the stack)
> 4. obtain a transpose of the G by reversing the direction of the edge.
> 5. while S is not empty perform step 6.
> 6. remove v = top of S and again perform DFS on it. The set of all visited vertices will give the strongly connected components containing v. Remove all visited vertices from stack.

<br>

**DFS-Loop**
```python
DFS-Loop(graph G):
  global variable t = 0
  global variable s = null
  
  assume nodes labelled 1 to n
  for i = n downto 1:
    if i not explored:
      s := i
      DFS(G, i)

DFS(graph G, node i):
  mark i as explored
  set leader(i) := node s
  for each arc (i, j) in G:
    if j not explored:
      DFS(G, j)
```