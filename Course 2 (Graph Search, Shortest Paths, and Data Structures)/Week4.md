Week 4
---

**Hash tables**
- running time: constant time
- supported operations (using a key)
  - insertion
  - deletion
  - look up

<br>

**Hash function**
- takes an input (a key) and spit out the an position in an array
- tells which position to store a given key
- good hash function spreads the data evenly amongst the buckets
<br>

**Resolving collisions**
1. Separate chaining
    - if two objects have same position, chain them together in same bucket of hash table (i.e. $$bucket(n) = x \rightarrow y \rightarrow z$$)
2. Open addressing *(linear probing)*
    - one object per bucket of the array
    - hash function is replaced by a hash sequence
    - keep try to fill the objective in following bucket (i.e. if bucket(3) is filled, try bucket(4) if also filled, try bucket(5). If it is empty, put into that bucket)
> h(k, 0) hash function for key k and first probe
> h(k, 1) hash function for key k and second probe
> h(k, 2) hash function for key k and third probe
> ...
> h(k, i) = (h(k) + i) mod m
> *i* indicates number of slots to skip for probe i
> *mod m* makes sure it is mapped overall to one of m slots in the hash table
> 
> it is easy to implement, however can result in primary clustering keys can cluster by taking adjacent slots in hash table, since each time serching for next available slot when there is collision. Results in longer search time.
3. Open addressing *(double hashing)*
    - have two hash functions
    - if first hash value failed, use second hash value to be an additive shift (i.e. first hash value = 6, second hash value = 3. If bucket(6) failed, try bucket(9), if it also failed, try bucket(12) and so on)

> if space is at a real premium, consider open addressing instead of chaining because chaining have excess memory
> however, deletion is tricker with open addressing than with chaining

<br>

**Hash table performance**
1. will get constant time lookup only if you keep the load constant. $$\alpha = 1$$
2. with opening addressing, need $$\alpha < 1$$

> load factor of the hash table, $$\alpha =$$ (# of elements (keys) in hash table) / (# of slots)
> $$$\alpha = \frac{n}{m}$$$
> when objects filled 75% of buckets, double the number of buckets. Therefore load factor will drop by factor of 2
> optionally, can also shrink the buckets from deletion

<br>

**Mathematically identify hash functions performance**
1. cryptographic hash functions
2. use randomization
    - design a family of hash functions
    - at run time, pick one of these hash functions at random

<br>

**Universal hash functions**
- refers to selecting a hash function at random from a family of hash functions with a certain mathematical property, it will gurantees a low number of collisions in expectation
- for each pair of distinct elements, the probability that they collide should be no larger than with the gold standard of perfectly uniform random hashing. (e.g. hash(x) and hash(y) from universe U $$\leq\ \frac{1}{m}$$)

> Let universal ($$\Phi$$) be a finite collection of hash functions that map a given universe (U) of keys into the range {0,1,2,...,m-1}
> $$\Phi$$, universal if for each pair of distinct keys x,y $$\in$$ U, the number of hash functions h $$\in\ \Phi$$ for which h(x) = h(y) is precisely equal to $$\frac{|\Phi|}{m}$$
> with a function randomly chosen from $$\Phi$$, the chance of a collision between x and y where x $$\neq$$ y is exactly $$\frac{1}{m}$$
> 
> **Example**
> let hash table size *m* be prime. Decompose a key x into r+1 bytes. (i.e., characters or fixed-width binary strings). Thus
> x = (x0, x1,..., xr)
> 
> assume that the maximum value of a byte to be less than *m*
> let a = (a0, a1,..., ar) denote a sequence of r+1 elements chosen randomly from the set {0,1,..., m-1}. Defined a hash function ha $$\in\ \Phi$$ by
> $$$
> ha(x) = \Sigma_{i=0}^{r}\ aixi\ mod\ m
> $$$
> with this definition, $$\Phi = \bigsqcup_a^{ha}$$ can be shown to be universal. Note that it has mr + 1 members.

<br>

**How to determine the hash function?**
- Division method, simple and fast implementation
    - any key wll indeed map to one of m slots
    - however, it needs to avoid certain values of m to avoid bias
    - often chosen in practice: m is a prime number and not too close to base of 2 or 10
> **example**
> h(k) = k mod m
> m = number of slots
> k = keys
> Example: m=20; k=91
> h(k) = k mod m = 11

<br>

**Bloom Filters**
- variant of hash table
- more space efficient than hash table
- **Drawbacks**
    - can't store an associated object
    - deletion are not allowed in most cases, it can be implemented but requires more work
    - can actually make mistakes (`false positive`, i.e. despite the fact you have never inserted given object, if you look it up later, it will says you have). However, having large array and more hash functions can reduce the probability of resulting `false positive`.

> Bloom filter have an array of n bits that stores (0 or 1) and hash function (or family of hash functions)
> 1. array of n bits, $$\frac{n}{|S|} =$$ # of bits per object in data set S.
> 2. k hash functions, h1,..., hk (k = small constant). Practically it is enough to use two diffeent hash function and then generate k different linear combinations of those two hash functions.
```javascript
function insert(x)
  for i=1,2,...,k
    set A[h:(x)] = 1

function lookup(x)
  return True <=> A[h:(x)]=1 for every i=1,2,...,k
```

> [read full explanation about Bloom Filters](http://www.geeksforgeeks.org/bloom-filters-introduction-and-python-implementation/)

<br>

**When to use Bloom Filters**
- tolerate to false positive rate in data
- really care about space efficiency

<br>

**Probability of false positivity in Bloom Filter**
- Let m be the size of bit array, k be the number of hash functions and n be the number of expected elements to be inserted in the filter, then the probability of false positive p can be calculated as
$$$
p = (1-[1-\frac{1}{m}]^{kn})^{k}
$$$

<br>

**Size of bit array in Bloom Filter**
- If expected number of elements n is known and desired false positive probability is p then the size of bit array m can be calculated as
$$$
m = -\frac{n\ ln\ p}{(ln2)^2}
$$$

<br>

**Optimum number of hash functions in Bloom Filter**
- The number of hash functions k must be a positive integer. If m is size of bit array and n is number of elements to be inserted, then k can be calculated as
$$$
k = \frac{m}{n}\ ln2
$$$

<br>
