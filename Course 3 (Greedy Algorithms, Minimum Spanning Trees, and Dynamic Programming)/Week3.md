Week 3
---

#### 01. Huffman Coding
- Build a Huffman Tree from input characters.
- Traverse the Huffman Tree and assign codes to characters.
- running time is $$O(n\ logn)$$ where n is the number of unique characters.

**Huffman Tree algorithm**
1. create a leaf node for each unique character and build a min heap of all leaf nodes.
2. extract two nodes with minimum frequency from the min heap.
3. create a new internal node with frequency equal to the sum of the two nodes frequencies. Make the first extracted node as its left child and the other extracted node as its right child. Add this node to the min heap.
4. repeat steps #2 and #3 until the heap contains only one node. The remaining node is the root node and the tree is complete.

**Average Encoding Length, $$L(T)$$**
$$$
L(T) = \Sigma_{i \in \Sigma}\ P_i \times [depth\ of\ i\ in\ T]
$$$
$$P_i$$ weight of each symbol, $$i$$ by its frequency

> complete Binary Tree has fixed length encoding
> Lopsided has has variable length encoding, which is optimized
>
> **Prefix Codes**
> set of binary sequence, P such that no sequence in P is a prefix of any other sequence in P.
> P = {01, 010, 10} is not a prefix code because 01 is a prefix of 010.
> P = {01, 100, 101} is a prefix code because 01 is not a prefix of 10 or 100 in second element and also it is not a prefix of 10 or 101 in third element.

<br>

#### 02. Dynamic Programming
Dynamic Programming is an algorithmic paradigm that solves a given complex problem by breaking it into subproblems and stores the result of subproblems to avoid computing the same results again. In general, given problems can be solved efficiently with Dynamic Programming
  1. Overlapping Subproblems
  2. Optimal Substructure

**Key ingredients of Dynamic Programming algorithm**
1. identify a small number of subproblems
2. can quicky and correctly solve "larger" subproblems given the solutions to "smaller subproblems"
3. after solving all subproblems, can quickly compute the final solution

> **Steps to solve a Dynamic Programming**
> 1) Identify if it is a DP problem
> 2) Decide a state expression with least parameters
> 3) Formulate state relationship
> 4) Do tabulation (or add memoization)
> 
> [Read Explanation](http://www.geeksforgeeks.org/solve-dynamic-programming-problem/)

<br>

#### 03. Overlapping Subproblems
*I.e., simple recursion to compute Fibonacci numbers*
```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)
```

There are two different ways to store the value so that it can be resued
  - Memoization (top down)
  - Tabulation (bottom up)

**Memoization** (top down)
The memoized program for a problem is similar to the recursive version with a small modification that it looks into a lookup table before computing solutions.

Algorithm
  1. initialize lookup array with all initial values as NIL
  2. whenever we need solution to a subproblem, look into the lookup table.
  3. if precomputed value is thee then return that value, otherwise calculate the value and put the result in lookup table so it can be reused later

*I.e., memoized version of Fibonacci number*
```python
def fib(n, lookup):
    if n == 0 or n == 1 :
        lookup[n] = n
    
    if lookup[n] is None:
        lookup[n] = fib(n-1 , lookup)  + fib(n-2 , lookup) 
 
    return lookup[n]
 
def main():
    n = 34
    lookup = [None]*(101)
    print "Fibonacci Number is ", fib(n, lookup)
```

**Tabulation** (bottom up)
The tabulated program for a given problem builds a table in bottom up fashion and returns the last entry from table.

For example, for the same Fibonacci number, we first calculate fib(0) then fib(1) then fib(2) then fib(3) and so on. So literally, we are building the solutions of subproblems bottom-up.

*I.e., tabulated version of Fibonacci number*
```python
def fib(n):
    f = [0] * (n+1)  # array declaration

    f[1] = 1  # base case assignment
 
    # calculating the fibonacci and storing the values
    for i in xrange(2 , n+1):
        f[i] = f[i-1] + f[i-2]

    return f[n]
 
def main():
    n = 9
    print "Fibonacci number is " , fib(n)
```

<br>

#### 04. Optimal Substructure
A given problems has Optimal Substructure Property if optimal solution of the given problem can be obtained by using optimal solutions of its subproblems.

For example, the Shortest Path problem has following optimal substructure property:
  - if a node x lies in the shortest path from a source node u to destination node v then the shortest path from u to v is combination of shortest path from u to x and shortest path from x to v.