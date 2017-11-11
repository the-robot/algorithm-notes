Week 1
---

**Course book names**
- CLRS,  Cormen, Leiserson, Rivest, and Stein, Introduction to Algorithms (3rd edition)
- DPV, Dasgupta, Papadimitriou, and Vazirani, Algorithms
- KT,  Kleinberg and Tardos, Algorithm Design
- SW,  Sedgewick and Wayne, Algorithms (4th edition)
<br/>

**Suggested Readings**
- CLRS, Chapters 2 and 3
- DPV, Sections 0.3, 2.1, 2.3
- KT, Sections 2.1, 2.2, 2.4, and 5.1
- SW, Sections 1.4 and 2.2
<br/>

**Part 1**  
- simple integer multiplication
  - greater than or equal to twice times operations
  - no. of operations $$<= const\ \times\ n^{2}$$
<br/>

**Part 2**  
- Karatsuba Multiplication
![Karatsuba Multiplication](https://i.imgur.com/TDubvbW.png)
<br/>

**Part 3 (Merge Sort Algorithm)**  
- Maximum no. of operation, $$<= 6n \times log_{2}n\ +\ 6n$$
- All selection, insertion, bubble sorts are calculated by quadratic functions of the input size. That is they need a constant times in the squared number of operations to sort an input array length of n
<br/>

**Part 4 (Merge Sort Analysis)**
![Recursion Tree of Merge Sort](https://i.imgur.com/UkErZmV.png)
- Recursion Tree
    - n = size of original array, j = level of the recursion tree
    - number of subproblem, $$2^{j}$$
    - size of array on j level, $$n/2^{j}$$
    - overall operation count, $$2^{j} \times 6(n/2^{j})$$. 6 is based on pseudocode
    - $$2^{j}$$ canceled each other so, $$6n$$ (independent of level j)
<br/>

**Part 5 (Asymptoptic Analysis Intro)**
- Asymptotic Notations are languages that allow us to analyze an algorithm's running time by identifying its behavior as the input size for the algorithm increases
- focus on running time for large input size n
- fast algorithm = worst case running time growly slowly with the input size
<br/>
- Example 1: Linear Search
    - check if there is given value in an array
    - $$O(n)$$
    ```python
    for i in array:
        if i is n: return True
    return False
    ```
- Example 2: Quadric Time Algorithm
    - check if there is common value in two nested loops
    - $$O(n^{2})$$
    ```python
    for i in array1:
        for j in array2:
            if i == j: return True
    return False
    ```
<br/>

**Extra Reading**
[Link About Big O Notation](http://discrete.gr/complexity/)  

- Asymptotic Behavior
    - filter of "dropping all factors" and of "keeping the largest growing term" is described as asymptotic behavior

- Θ(here) means time complexity or just complexity of algorithm
    - Θ(1) = constant-time algorithm
    - Θ(n) = linear
    - Θ(n2) = quadratic
    - Θ(log(n)) = logarithmic
> Programs with a bigger Θ run slower than programs with a smaller Θ

| Asymptotic comparison operator | Numeric comparison operator |
|:------------------------------:|:---------------------------:|
| Our algorithm is o( something )| A number is < something     |
| Our algorithm is O( something )| A number is ≤ something     |
| Our algorithm is Θ( something )| A number is = something     |
| Our algorithm is Ω( something )| A number is ≥ something     |
| Our algorithm is ω( something )| A number is > something     |

