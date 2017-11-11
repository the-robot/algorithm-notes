Week 3
---

**Suggest Readings**
- Algorithms Illuminated (Part 1), Chapter 5 and Appendix B

**Quicksort Algorithm**
- best case: $$\Theta(n\ log(n))$$
- worst case: $$\Theta(n^{2})$$
```python
QuickSort(array A, length n)
    if n = 1 return
    p = ChoosePivot(A, n)
    Partition A around p
    
    recursively sort 1st partition
    recursively sort 2nd partition
```

<br/>

- Choosing pivot
    - choose random pivot for every recursive call
    - if always get 25-75 split or better, good enough for $$O(n\ log(n))$$

<br/>

**Sample Space ($$\Omega$$)**
- all possible outcomes
- in algorithms, $$\Omega$$ is finite
- each outcome is $$i \in \Omega$$ has a probability $$p(i) \geq O$$

<br/>

**Events ($$S$$)**
- subset of sample space $$\Omega$$, $$S \subset \Omega$$
- probability of event is sum of the probabilities of all the outcomes contained in that event
- $$S = \Sigma_{i \in S}\ p(i)$$

<br/>

**Random Variables ($$X$$)**
- statistic measuring what happens in the random outcome
- real-valued function defined on the sample space, $$\Omega$$
- $$X:\Omega \rightarrow R$$

<br/>

**Expectation ($$E[X]$$)**
- let $$X:\Omega \rightarrow R$$ be a random variable, $$X$$
- expectation, aka expected value $$E[X]$$ of $$X$$ = average value of X
- $$= \Sigma_{i \in \Omega}\ X(i) \times p(i)$$, sum over everything that could happen

<br/>

**Linearity of Expectation $$[LIN\ EXP]$$**
- $$E[\Sigma^{n}_{i=1}\ X{i}] = \Sigma^{n}_{i=1}\ E[X_{i}]$$
- property that the expected value of the sum of random variables is equal to the sum of their individual expected values, regardless of whether they are independent
- $$E[X + Y] = E[X] + E[Y]$$

> $$E[XY] ::= \Sigma_{x, y}xy\ Pr[X=x$$ AND $$Y=y]$$
> $$=\Sigma_{x, y}xy\ Pr[X=x]Pr[Y=y]$$
> $$=\Sigma_{y}\ \Sigma_{x}xy\ Pr[X=x]Pr[Y=y]$$
> $$=\Sigma_{y}(y\ Pr[Y=y]\Sigma_{x}x\ Pr[X=x])$$
> $$=(\Sigma_{x}x\ Pr[X=x])(\Sigma_{y}y\ Pr[Y=y])$$
> $$=E[X]E[Y]$$
> 
> $$\therefore E[XY] = E[X]E[Y]$$

`Rules`
- *don't assume product rule without independence*
- $$E[\frac{x}{y}] \neq \frac{E[x]}{E[y]}$$ 
- if X and Y are not independent, $$E[XY] \neq E[X] \times E[Y]$$

<br/>

**Conditional Probability**
- (X givens Y), $$Pr[X|Y] = \frac{Pr[X \cap Y]}{Pr[Y]}$$

<br/>

**Independence (of Events)**
- Events $$X, Y \leq \Omega$$ are independent
- if and only if $$Pr[X \cap Y] = Pr[X] \times Pr[Y]$$
- $$Pr[X|Y] = Pr[X] \leftrightarrow Pr[Y|X] = Pr[Y]$$

<br/>

**Independence (of Random Variables)**
- the events of the two variables taking on any given pair of values are independent events
- random variables $$A, B$$ (both defined on $$\Omega$$)
- independent if and only if events $$Pr[A=1], Pr[B=b]$$ are independent of all a,b
- $$\leftrightarrow Pr[A=a\ and\ B=b] = Pr[A=z] \times Pr[B=b]$$
- if $$A, B$$ are independent, then $$E[AB] = E[A] \times E[B]$$

<br/>

**Building Blocks**
- $$z_{i} = i^{th}$$ smallest element of array, $$A$$
- random variable $$X_{ij}(\sigma) = \#$$ of times $$z_{i}, z_{j}$$ get compared in QuickSort with pivot sequence $$\sigma$$

<br/>

**Decomposition Approah**
- Steps
    - identify random variable Y that you really care about
    - express Y as sum of indicator random variable, $$C = \Sigma_{l=1}^{m}\ X_{e}$$
    - apply linearity of expecatation, $$E[Y] = \Sigma_{l=1}^{m}\ Pr[X_{e}=1]$$

- $$C(\sigma) = \#$$ of comparisons between input elements
- $$X_{ij}(\sigma) = \#$$ of comparisons between $$z_{i}$$ and $$z_{j}$$
- $$\therefore\ \sigma, C(\sigma) = \Sigma_{i=1}^{n-1}\ \Sigma_{j=i+1}^{n}\ X_{ij}(\sigma)$$