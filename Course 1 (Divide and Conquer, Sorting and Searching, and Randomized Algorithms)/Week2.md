Week 2
---

**Suggested Readings**
- CLRS, Chapter 4 (except Section 4.3), and Sections 28.1 and 33.4
- DPV, Sections 2.2 and 2.5
- KT, Sections 5.2-5.5
<br/>

**Divide and Conquer Paradigm**
1. Divide into smaller subproblems
2. Conquer via recursive calls
3. Combine solutions of subproblems into one for the original problem
<br/>

**Brute Force Algorithm for Inversion Check**
- Runtime: $$O(n^{2})$$
- Nested for loop to check one (Array1[i]) by one (Array2[j]).
<br/>

**Divide and Conquer Algorithm for Inversion Check**
- assumed $$i < j$$ 
- Left inversion if $$i, j \leq \frac{n}{2}$$
- Right inversion if $$i, j > \frac{n}{2}$$
- Split inversion if $$i \leq \frac{n}{2}$$ and $$j > \frac{n}{2}$$
<br/>

**Strassen's Subcubic Matrix Multiplication Algorithm**
$$$
X = \left(\begin{array}{cc} 
A & B\\
C & D
\end{array}\right)

\ Y = \left(\begin{array}{cc} 
E & F\\ 
G & H
\end{array}\right)
$$$
- Seven Products
    - $$P_{1} = A(F-H)$$
    - $$P_{2} = (A+B)H$$
    - $$P_{3} = (C+D)E$$
    - $$P_{4} = D(G-E)$$
    - $$P_{5} = (A+D) \times (E+H)$$
    - $$P_{6} = (B-D) \times (G+H)$$
    - $$P_{7} = (A-C) \times (E+F)$$

$$$
X \times Y = \left(\begin{array}{cc}
(P_{5}+P_{4}-P_{2}+P_{6}) & (P_{1}+P_{2})\\
(P_{3}+P_{4}) & (P_{1}+P_{5}-P_{3}-P_{7})
\end{array}\right)
$$$
<br/>

**Algorithm for Closest Pair**
- Distance between two points, $$\sqrt{(x_{1}-y_{1})^{2} + (x_{2}-y_{2})^{2}}$$
<br/>

**The Master Method**
- blackbox method for solving recurrences
- Assumptions
    - all subproblems have exactly same size

1. Base case: $$T(n) \leq a (constant)$$ for all sufficiently small n.
2. For all larger n
    - $$T(n) \leq aT(\frac{n}{b}) + O(n^{d})$$
    - a = number of recursive calls ($$\geq 1$$)
    - b = input size shriking factor ($$> 1$$)
    - d = exponent in running time of "combine step" (outside recursive call, $$\geq 0$$)
    - a, b, and d are independent from input size n

- Master method three cases, T(n)
    - $$a = b^{d}$$, running time $$O(n^{d} log n)$$
    - $$a < b^{d}$$, running time $$O(n^{d})$$
    - $$a > b^{d}$$, running time $$O(n^{log_{b}a})$$
