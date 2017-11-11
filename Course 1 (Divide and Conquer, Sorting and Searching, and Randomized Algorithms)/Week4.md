Week 4
---

**Suggested Readings**  
- Algorithms Illuminated (Part 1), Chapter 6

<br>

**Order of Statistic**  
- $$i^{th}$$ order of statistic = $$i^{th}$$ smallest element in an array

<br>

**Reduction to Sorting**
- solve problem by reducing it to another problem that we already know
- *Example*
    - find $$i^{th}$$ smallest element in an array by
    - sorting with merge sort $$O(n\ log(n))$$, and find $$i^{th}$$ smallest by index

<br>

**Randomized Selection**  
```python
Rselect(array A, length n, order statistic i)
    if n=1, return A[1]
    choose pivot p from A uniformly at random
    partition A around p
    let j = new index of p

    if j=i, return p
    if j>i, return Rselect(1st part of A, j-1, i)
    if j<i, return Rselect(2nd part of A, n-j, i-j)
```

<br>

**Graphs**
- Vertex (Vertices), aka nodes (V)
- Edges (E) = pairs of vertices
  - can be undirected pairs, (unordered pair)
  - directed pairs (ordered), aka Arcs

> dots refer to vertices
> edges are line

<br>

**Cuts of Graphs**
- a cut of a graph (V, E) is a partition of V into two non-empty sets A and B

![cuts_of_graphs.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/yz379wvbjoytx1or.png)

- corssing edges of a cut (A, B) are thoese with
  - one endpoint in each of (A, B) *[undirected]*
  - tail with A, head in B *[directed]*

<br>

**The Minimum Cut Problem**
- find fewest number of crossing edges
- an undirected graph $$G = (V, E)$$

![min_cut_problem.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/e7og218gckvjkyb9.png)

- Usage
  - identity network bottlenecks/weaknesses
  - community detection in social networks
  - image segmentation (input = graph of pixels)
    - use edge weights (weight of an edge is how likely you expect those two pixels to come from same object)

<br>

**Graph size**
- number of vertices (n)
- number of edges (m)

<br>

**Sparse vs. Dense Graphs**
- let $$n = \#$$ of vertices, $$m = \#$$ of edges
- in most applications, $$m = \Theta(n)$$ and $$O(n^{2})$$
- sparse means closer to lower bound / linear
- dense mean closer to upper bound / quadratic

<br>

**Adjacency Matrix**
- an adjacency matrix is a square matrix used to represent a finite graph. The elements of the matrix indicate whether pairs of vertices are adjacent or not in the graph
- represent $$G$$ (graph) denoted by A, where $$A_{ij}=1 \leftrightarrow G$$ has an i-j edge
- $$A_{ij}$$ = # of i-j edges (if parallel edges)
- $$A_{ij}$$ = weight of i-j edges (if any)
- $$A_{ij}$$ = +1 $$i \rightarrow j$$ or -1 if $$i \leftarrow j$$
- running time: $$O(V^{2})$$

![example1.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/4kfgwdwkjaq93sor.png)

![example2.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/lu97ars5fjrftj4i.png)

<br>

**Adjacency Lists**
- array (or list) of vertices
- array (or list) of edges
- each edge points to its endpoints
- each vertex points to edges incident on it
- running time: $$O(V + E)$$

<br>

**Random Contraction Algorithm**
```python
while there are more than 2 vertices
  pick a remaining edge (u,v) uniformly at random
  merge (or "contract") u and v into single vertex
  remove self-loops
return at represented by final 2 vertices
```

![image.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/4mkhp586lh0py14i.png)

![image.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/t2yse9tid4w019k9.png)

<br>

#### [Min-Cut Algorithm Explanation Tutorial](http://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)

