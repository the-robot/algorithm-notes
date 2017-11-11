Week 1
---

#### 01. Needleman-Wunsch score
- can find similarity between two string

<br>

#### 02. Greedy algorithm
- Greedy algorithm is an algorithm that follows the problem solving heuristic of making the locally optimal choice at each stage with the hope of finding a global optimum.
- make sequence of decisions with each decision being made myopically
- **Exchange Argument** is one of the method to perform proof of correctness (PoC) to greedy algorithm
<br>

#### 03. Scheduling problem
- one shared resource (e.g., processor)
- many "jobs" to do on that shared resource
- assume each job j has
  - weight, $$w_j$$ ("priority")
  - length, $$l_j$$ ("time required to complete the job")

**Completion time**
completion time, $$C_j$$ of job, j = sum of job lengths up to and including j.
$$$completion\ time = \Sigma_{j=1}^n w_j C_j$$$

example
| Job | Length | Weight |
|:---:|:------:|:------:|
| job 1 | 1 | 3 |
| job 2 | 2 | 2 |
| job 3 | 3 | 1 |

$$$completion\ time = 3 \times 1\ +\ 2 \times (2 + 1)\ +\ 1 \times (3+2+1)$$$
$$$\therefore\ ans = 15$$$

**Goal of scheduling job**
minimize the weighted sum of completion time
$$$min(completion\ time)$$$

> **2 rules for scheduling advice**
> - if jobs have same weight but different length, do the job with smaller length first
> - if jobs have same length but different weight, do the job with larger weight first

<br>

#### 04. Minimum spanning tree algorithm
- input would be undirected graph, $$G = (V, E)$$
  - $$V$$ stands for vertices
  - $$E$$ stands for edges
- cost $$C_e$$ for each edge, $$e \in E$$
- edges can be either positive or negative
- output will be the minimum cost tree $$T \leq E$$ that spans all vertices
- cost means summing up the edges in the tree that we output

**sub graph, $$T$$**
- cannot have any loops in a tree
- contain path between each pair of vertices

<br>

#### 05. Prim's MST Algorithm
- running time: $$O(nm)$$
- it can be speed up via heap data structure, $$O(m\ log n)$$
```python
# V is a list that contains all vertices
X = [S]  # [S in V chosen arbitrarily]
T = []   # [invariant: X = vertices spanned by tree-so-far T]

while X != V:
  let e = (u, v) be the cheapest edge of G with u in X, v not in X
  add e to T
  add v to X
```

- optimized Prim's algorithm with Heap data structure
```python
Algorithm prim(G = (V, E, length): edge-weighted graph, s in V)
S = set of nodes, initially empty
dist: array[V] of integer, initially infinity
prev: array[V] of V, initially nil

H: heap of edges, prioritized by dist, initially {s}
dist[s] = 0

while H is not empty:
  u = deletemin(H), add u to S
  for each u in (V - S):
    
    if w(u,v) < dist[v]:
      dist[w] = length(v, w)
      prev[w] = v
      insert(v, H)
```

> there is a similarity between Prim's algortihm and Dijkstra's algorithm. The only difference is that in Dijkstra's algorithm we prioritize nodes according to their distance from the *single node s*, while in Prim's algorithm we prioritize them according to their distance from the *set of nodes S*.
> 
> for this reason, the running time of Prim's algorithm is clearly the same as the Dijkstra's algorithm, since the only change is the definition of the key under which the heap is ordered. Thus, if we use d-heaps, the running time of Prim's algorithm is $$O(m\ log_{2+m/n}n)$$

#### 06. Cuts
- a cut of a graph, $$G = (V, E)$$ is a partition of $$V$$ into 2 non-empty sets
![DeepinScreenshot_select-area_20171104035745.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/qv0auzw7fnku766r.png)

**Empty Cut Lemma**
- a graph is not connected, no crossing edges

**Double-Crossing Lemma**
- suppose the cycle $$C \subseteq E$$ has an edge crossing the cut $$(A, B)$$: then so does some other edge of $$C$$
![DeepinScreenshot_select-area_20171104043200.png](https://raw.githubusercontent.com/Hadesy2k/algnotes/master/images/h60eokqzgotdfgvi.png)

**Lonely Cut Corollary**
- if $$e$$ is the only edge crossing some cut $$(A, B)$$, then it is not in any cycle
- if it were in a cycle, some other edge would have to cross the cut

**Cut Property**
- consider an edge $$e$$ of $$G$$, suppose there is a cut $$(A, B)$$ such that $$e$$ is the cheapest edge of $$G$$ that crosses it.
- e belongs to the MST of $$G$$