Week 3
---

**Data Structures**
- in general, fewers operations the data structure supports the faster the operation will be and smaller the space overhead required by data strcuture

<br>

**Heap Data Structure**
- supports insertion and extracting mininum/maximum key value

*Heapify*, initialize heap in linear time, $$O(n)$$
*Delete*, not just minimum, also arbitrary elements from the middle of a heap in $$O(logn)$$

When to use
- program is doing repeated minimum computations, esp via exhaustive search (e.g. selection sort)

> read Week 2 notes for details of Heap data structure

<br>

**Heap Sort**
- comparison based sorting algorithm
- $$O(n\ logn)$$

<br>

**Difference between Heap and Binary Search Tree**
- Heap just guarantees that elements on higher levels are greater (for max-heap) or smaller (for min-heap) than elements on lower levels, whereas BST guarantees order (from "left" to "right"). If you want sorted elements, go with BST.
- Heap is better at findMin/findMax (O(1)), while BST is good at all finds (O(logN)). Insert is O(logN) for both structures. If you only care about findMin/findMax (e.g. priority-related), go with heap. If you want everything sorted, go with BST.

<br>

**Binary Search Tree**
- $$O(logn)$$ running time
- BST can be considered as dynamic version of sorted array
- each node in tree have three pointers
  - first points to parent node
  - second points to left child node
  - third points to right child node
  - one or two of the pointers can be `null` but not all
- parent node is a key
- all nodes in left child $$\leq$$ key node and all nodes in right child $$\geq$$ key node

![DeepinScreenshot_select-area_20171028152702.png](/:storage/201syawm3ht73nmi.png)

| Operation | Running time |
|:---------:|:------------:|
| Search | $$O(logn)$$ |
| Select | $$O(logn)$$ |
| Min/Max | $$O(logn)$$ |
| Pred/Succ | $$O(logn)$$ |
| Rank | $$O(logn)$$ |
| Insert/Delete | $$O(logn)$$ |

<br>

**Finding Min, Max in Binary Search Tree**
- start at root
- follow left (minimum) or right (maximum) child pointers until you can't follow anymore (when null pointer is met), then return last key found

<br>

**Computing predecessor in Binary Search Tree**
```python
if k left subtree is not empty:
  return max key in left subtree

if k left subtree is empty:
  follow parent pointers until that parent pointer key is less than k
  return that parent pointer key

# replace left with right for computing successor 
```

<br>

**In-order traversal of Binary Search Tree**
- $$O(n)$$ running time
```python
inorder(tree):
  traverse left subtree, call inorder(left-subtree)
  visit root
  traverse right subtree, call inorder(right-subtree)
```

<br>

**Deletion in Binary Search Tree**
- $$O(height of the tree)$$ running time
```python
if k has no child:  # easy case
  just delete k from tree

if k has one child:  # medium case
  delete k and replace it's child position to k

if k has both child:  # hardest case
  compute k's predecessor (from left child node)
  # follow k's left child until null is met on left child
  # then follow last left child's right child until no longer possible
  # it is the predecessor
  swap k and it's predecessor
  delete k from tree
```
<br>

**Select and Rank**
- $$O(height of the tree)$$ running time 
```python
start at root x, with children y and z
let a = size(y)  # a = 0 if x has no left child

if a = i-1:
  return x's key

if a >= i:
  recursively compute (i)th order statistic of search tree rooted at y

if a < i-1:
  recursively compute (i-a-1)th order statistic of search tree rooted at z
```

<br>

**Red-Black trees**
- balanced binary search tree
> see also `splay trees` aka self-adjusting trees, `B/B+ trees`, `AVL trees`

<br>

**Red-Black invariants**
1. each node is either red or black
2. root is black
3. no 2 reds in a row
    - if there is a red node in search tree, then it's children must be black
4. every path you might take from a root to a null pointer (e.g. unsuccessful search), passed through exactly same number of black nodes

> if all of these four invariants are satisfied in search tree, then the height of the tree is going to be small
> height will be no more than double the absolute minimum that we can conceivably have, $$\leq\ 2\ logn$$

<br>

**Left rotations**
- runs in constant time (constant number of pointers)
- locally re-balance a search tree, without vilating the search tree properties
![DeepinScreenshot_select-area_20171028235559.png](/:storage/cz4m1fm0cazl4n29.png)

<br>

**Right rotations**
- right rotation is the inverse of left rotation
![DeepinScreenshot_select-area_20171028235751.png](/:storage/lm8icmhlqmcs1yvi.png)