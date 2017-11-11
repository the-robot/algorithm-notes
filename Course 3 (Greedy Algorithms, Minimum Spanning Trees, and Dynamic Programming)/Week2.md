Week 2
---

#### 01. Kruskal's MST Algorithm
**Procedure**
- choose an edge the smallest cost in every iteration
- however, do not choose an edge if it will create cycle
- if there are parallel edges, throw out the expensive edges and only keep the cheapest one
- naive running time: $$O(mn)$$
- running time with union-find data structure: $$O(m\ logn)$$
  - each $$x \in X$$ points directly to the "leader" of its group
  - $$O(1)$$ find operation (return x' leader)
  - $$O(nlogn)$$ for union operation (2 groups merge, smaller group inherit leader of larger group)

> Union-Find Algorithm can be used to check whether an undirected graph contains cycle or not in constant time. $$O(1)$$
> 
> It can see whether adding new edge would create a cycle in an undirected graph. When two ind operations returned the same answer, we can conclude that there will be a cycle.
>   - why? because if and only if the end points of the given edge were already in the same connected component.

```python
sort edges in order of increasing cost  # [1, 2, 3,..., m]
T = []  # MST

for i = 1 to m:
  if T in {i} has no cycle:
    add i to T

return T
```

- optimized Kruskal's algorithm with Union-Find

```python
Algorithm kruskal(G = (V, E, w): edge-weighted graph)
X: set of edges, initially empty
E = sort E in increasing length

for each v in E:
  MAKESET(v)

for [u, v] in E (in increasing order):
  if FIND(u) != FIND(v):
    add edge [u, v] to X
    UNION(u, v)
```

> Extra note: Karger-Klein-Tarjan's Algorithm is randomized algorithm and faster than both Prim's and Kruskal Algorithm and its running time is linear. $$O(m)$$
> $$O(m\ \alpha(n))$$ deterministic. $$\alpha$$, Inverse Ackerrmann function is very slow growing function.

- Kruskal's algorithm for Maximum Spanning Tree

```javascript
// initialize the vertex and edge for graph
vertex = Set of vertices
ed = Set of edges

// pass the parameter as "vertex" and "ed" to
// maximumtree function
return maximumtree(vertex, ed)


// define the maximumtree() function
function maximumtree(vertex, ed) {
    // loop executes until the "ed"
    for edge in ed:
        // set all the edge weight as "negative edge //weight"
        edge.w_e = -edge.w_e


    // calcuate the minimum spanning tree by calling
    // Kruskal's and store the result into "mst"
    mst = Kruskals(vertex, ed)

    // store the edge "ed" to "max" variable
    max = ed

    // loop executes until the minimum edges in minimum
    // spanning tree "mst"
    for edge in mst.edge:

        // remove the minimum edge from the "max"
        max.remove(edge)


    // return the "max" variable which contains the
    // maximum edge weight
    return max
}
```

<br>

#### 02.k-Clustering
- k is # of clusters desired
- in practice, run experiments with different k values and select the desire one

```python
# single-link clustering
initially, each point in a separate cluster
repeat until only k clusters:
  let p, q = clostest pair of separated points
  # determined by the current spacing
  merge the clusters containing p & q into a single cluster
```

<br>

#### 03. Union-Find Data Structure
A disjoint-set data structure is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets. A union-find algorithm is an algorithm that performs two useful operations on such a data structure:
1. FIND: Determine which subset a particular element is in. This can be used for determining if two elements are in the same subset. It returns the leader of the group, you can find the leader by traversing parent pointers from x until you get to a root (object that points back to itself).
2. UNION: Join two subsets into a single subset. Given two objects x and y, you have to find their respective roots so have to invoke the FIND operation twice, once for x to get its root s1 and once for y to get its root s2. Then merge by install either s1 or s2 as a child of the other.

<br>

#### 04. Eager Union
- every objects point to new leader in each merge
- leader of smaller group also points to the leader of larger group

<br>

#### 05. Lazy Union
- update only one pointer in each merge
- the leader of one group points to the leader of another group

**Pro**
- UNION reduces to 2 FIND operations and $$O(1)$$ extra work for changing pointer of smaller group's leader.

**Con**
- parent pointers do not point directly to roots
- have to traverse in general a sequence of parent pointers from a given object x to go all the way up to the root of the correspondence tree
- not clear if FIND still takes $$O(1)$$ times

<br>

#### 06. Union by Rank
- for all x $$\in$$ X, rank[x] = maximum nubmer of hops required to get from a leaf of x's tree up to x itself
- rank of the node x from its child y is rank of y + 1

**to avoid scraggly trees**
```python
s1 = FIND(x), s2 = FIND(y)
if rank[s1] > rank[s2] then set parent [s2] to s1,
else set parent[s1] to s2
```

<br>

#### 07. Path Compression
- when FIND is invoked from some node x, and traverse parent pointers from x up to its root, r. For every object that visited along along this path from x to r, rewire the parent pointer to point directly to r.
- anything below the root and its immediate descendents on this path from x will have its parent pointer updated and it'll be updated to point directly to r.

> ranks are **untouched** by path compression.

<br>

#### 08. Hopcroft-Ullman Theorem
- consider a union find data structure implemented in Lazy Unions, Union by Rank, Path Compression. Consider an arbitrary sequence of m FIND, and UNION operations, and suppose the data structure contains n objects, then the total work the data structure does to process this entire sequence of m operations is
$$$
O(m\ log*n)
$$$
where $$log*n$$ = the number of times you need to apply log to n before the result is $$\leq$$ 1.

> $$log*n$$ is a really slow growth function.

<br>

#### 09. The Ackermann Function
- function that incredibly, grows still more slowly than $$log*n$$ function
- $$A_k(r)$$ for all integers where $$k \geq 0$$ and $$r \geq 1$$ (recursively)
- Base case: $$A_0(r) = r + 1$$ for all $$r \geq 1$$
- $$A_0(r)$$ is successor function

> for $$k, r \geq 1$$:
> $$A_k(r)$$ = apply $$A_{k-1}$$ r times to r, $$(A_{k-1}...)(r)$$
> 
> $$A_0(r)$$ is successor function, $$\rightarrow r+1$$
> $$A_1(r)$$ is doubling function, $$\rightarrow 2r$$
> $$A_2(r)$$ is exponentation function, $$\rightarrow r2^{r}$$
> $$A_n(r)$$ is tower function, $$\rightarrow 2^{2^{.. r\ times ..^{2}}}$$, also known as "wowzer function"
> 
> Example
> what is $$A_3(2)$$?
> $$$A_3(2) = A_2(A_2(2))$$$
> $$$= A_2(2 \times 2^{2})$$$
> $$$= A_2(8)$$$
> $$$= 8 \times 2^{8}$$$
> $$$= 2^{3} \times 2^{8}$$$
> $$$= 2^{11}$$$
> $$$= 2048$$$

<br>

#### 10. The Inverse Ackermann Function
- to define inverse, one parameter either k or r need to be fixed
- for this case, r is fixed as $$r = 2$$
- for every $$n \geq 4$$
- $$\alpha(n) =$$ minimum value of $$k$$ such that $$A_k(2) \geq n$$

> $$\alpha(n) = 1$$ for $$n = 4$$ because $$A_1(2) = 4$$
> 
> $$\alpha(n) = 2$$ for $$n = 5,6,7,8$$ because $$A_2(2) = 8$$. $$A_2(2)$$ is sufficient to map 2 to a number at least as big as 8.
> 
> $$\alpha(n) = 3$$ for $$n = 9,...,2048$$ because $$A_3(2) = 2048$$. $$A_3(2)$$ is sufficient to map 2 to a number up to 2048.