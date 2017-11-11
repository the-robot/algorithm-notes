Week 2
---

**Dijkstra's Shortest Path Algorithm**
- works on any directed graph with non negative edge length
- uses heap data structure
- O(n log n)
```python
X = [s]  # vertices processed so far
A[s] = 0  # computed shortest path distances

while X != V:  # main loop
  among all edges (v,w) in E with v in X and w not in X
  pick the one that minimizes
  
  A[v] + length(vw)  # Dijkstra's greedy criteria
  add w* to X
  set A[w*] := A[v*] + length(v*w*)
```
> if the length of all edges are the same, it becomes BFS

 <br>
 
**Heap data structure**
 - Heap is a special case of balanced binary tree data structure where the root-node key is compared with its children and arranged accordingly.

- Min-Heap, where the value of the root node is less than or equal to either of its children
![min_heap_example.jpg](/:storage/5jkp0hqlmnsl9pb9.jpg)


- Max-Heap, where the value of the root node is greater than or equal to either of its children
![max_heap_example.jpg](/:storage/51swwdcktob0rudi.jpg)

<br>

**Max Heap Construction Algorithm**
1. create a new node at the end of heap
2. assign new value to the node
3. compare the value of this child node with its parent
4. if value of parent is less than child, then swap them
5. repeat step 3 & 4 until Heap property holds

> in Min Heap construction algorithm, we expect the value of the parent node to be less than that of the child node
 
![max_heap_animation.gif](/:storage/rwa9qrkzzw9g4x6r.gif)

<br>

**Max Heap Deletion Algorithm**
1. remove root node
2. move the last element of last level to root
3. compare the value of this child node with its parent
4. if value of parent is less than child, then swap them
5. repeat step 3 & 4 until Heap property holds

> Deletion in Max (or Min) Heap always happens at the root to remove the Maximum (or minimum) value

![max_heap_animation.gif](/:storage/h6y6yj399dswz5mi.gif)

<br>

**Array Implementation of Heap**
```python
parent(i):
  if i is even:
    parent = position of i/2
  
  if i is odd:
    parent = floor(position of i/2)
```
![DeepinScreenshot_select-area_20171028024744.png](/:storage/244fjcctzfamj9k9.png)

<br>

**Faster Dijkstra's Shortest Path Algorithm**
- use Heap data structure
- store vertices on heap
- traverse all vertices of graph using BFS and use a Min Heap to store vertices not yer included in Shortest Path Tree
- Min Heap is used as a priority queue to get the minimum distance vertex from set of not yet included vertices

> **Procedure**  
> 1. create a Min Heap of size V where V is number of vertices in the given graph. Every node of min heap contains vertex number and distance value of the vertex
> 2. initialize Min Heap with source vertex as root (the distance value assigned to source vertex is 0). The distance value assigned to all other vertices is infinite
> 3. While Min Heap is not empty
> > - extract vertex with minimum distance value node from Min Heap. Let the extracted vertex be u
> > - for every adjacent vertex v of u, check if v is in Min Heap. If v is in Min Heap and distance value is more than weight of u-v plus distance value of u, then update the distance value of v.