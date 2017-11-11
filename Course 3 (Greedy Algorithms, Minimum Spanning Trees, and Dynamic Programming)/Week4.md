Week 4
---

#### 01. Knapsack Problem
**Formal Definition**
- whenever you have sort of a budget of a resource that you can use, and you want to use it in smartest way possible. That's basically the knapsack problem.

**Example Problem**
- For given weights and values of n items, and total available knapsack capacity, find the maxium value subset which sum of the weights does not exceed the knapsack capacity.

**Simple Example**
weight = [3, 6, 4]
value = [60, 100, 120]

item A = weight 3, value 60
item B = weight 6, value 100
item C = weight 4, value 120
knapsack capacity = 10

maximum value subset = item B + item C $$\rightarrow$$ 6 + 4 $$\rightarrow$$ 9
item B + item C $$\geq$$ knapsack capacity, 10
value = 120 + 100 $$\rightarrow$$ 220

**Optimal Substructure**
To consider all subsets of items, there can be two cases for every item: (1) the item is included in the optimal subset, (2) not included in the optimal set. Therefore, the maximum value that can be obtained from n items is max of following two values
  1. Maximum value obtained by n-1 items and W weight (excluding nth item).
  2. Value of nth item plus maximum value obtained by n-1 items and W minus weight of the nth item (including nth item).

*If weight of nth item is greater than W, then the nth item cannot be included and case 1 is the only possibility.*

![IMG_20171110_191501_01.jpg](/:storage/uawdddbpgsvbcsor.jpg =500x)

<br>

**Naive Knapsack algorithm**, running time is exponential. $$O(2^n)$$
```python
# returns the maximum value that can be put in a knapsack of
def knapSack(W , wt , val , n):
    # W, knapsack capacity
    # wt, weight of each item
    # val, value of each item
    # n, number of items

    # base case
    if n == 0 or W == 0 :
        return 0

    # check if current item's weight is greater than the weight
    # we have. If it is, then we cannot include an item
    if (wt[n-1] > W):
        return knapSack(W , wt , val , n-1)

    # return the maximum of two cases:
    # (1) nth item included
    #     - current item's value
    #     - +
    #     - weight reduced by current item's weight and
    #       starting from next item onwards
    #
    # (2) not included
    #     - exclude current item
    #     - keep the weight limit same and
    #       starting from next item onwards
    else:
        return max(val[n-1] + knapSack(W-wt[n-1], wt, val, n-1),
                   knapSack(W, wt, val, n-1))

val = [60, 100, 120]
wt = [3, 6, 4]
W = 10
n = len(val)

print knapSack(W , wt , val , n)
```

> [watch naive algorithm explanation video](https://www.youtube.com/watch?v=ipRGyCcbrGs)

<br>

**Dynamic Programming version of Knap Snap Algorithm**, $$O(nW)$$
- $$K[i][0]\ = 0\ \forall\ i\ belongs\ to\ [0, N]$$
- $$K[0][w]\ = 0\ \forall\ w\ belongs\ to\ [0, W]$$

2 intermediate cases will be then
- $$K[i][w] = K[i-1][w]$$
- $$K[i][w] = max(\ value[i] + K[i-1][w - weight[i]],\ K[i][w]\ )\ \forall\ i, w$$

Final answer will be $$K[n][W]$$, i.e. maximum profit achieved by considering $$N$$ items such that you had atmost $$W$$ units of space filled in the bag.

```python
# used Tabulation method
def knapSack(W, wt, val, n):
    # W, knapsack capacity
    # wt, weight of each item
    # val, value of each item
    # n, number of items

    # create n+1 numbers of W+1 size list 
    # K[i][w] denoting the maximum profit earned by considering first i items
    # and having atmost w units of bag filled.
    K = [[0 for x in range(W+1)] for x in range(n+1)]

    # first list of K and first element of every K will be 0
    # i indicates the item
    for i in range(1, n+1):
        for w in range(1, W+1):
            if wt[i-1] <= w:
                # max of result values obtained from when that item is included
                # and when that item is not included
                K[i][w] = max(val[i-1] + K[i-1][w-wt[i-1]],  K[i-1][w])

            else:
                # if weight is greater than max possible weight
                # it should be left, obviously
                K[i][w] = K[i-1][w]

    # return last element of last array, K[3][10]
    return K[n][W]
 
val = [60, 100, 120]
wt = [3, 6, 4]
W = 10
n = len(val)


# K[0] = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
# K[1] = [0, 0, 0, 60, 60, 60, 60, 60, 60, 60, 60]
# K[2] = [0, 0, 0, 60, 60, 60, 100, 100, 100, 160, 160]
# K[3] = [0, 0, 0, 60, 120, 120, 120, 180, 180, 180, 220]

print knapSack(W, wt, val, n)
```

<hr>
<br>

#### 02. Sequence Alignment Problem
Sequence alignment problem is to compute a similarity measure between strings, a similarity measure defined as the total penalty of the best alignment (aka. **Needleman-Wunsch score**)

In general we evaluate the alignment by summing up the penalties of all the flaws
- the sum penalty per gap
- the sum penalty per mismatch

**example**

| A | G | G | G | C | `T` |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| A | G | G | `-` | C | `A` |

total penalty = $$\alpha_{gap} + \alpha_{AT}$$

> gaps can be inserted to both of the strings

<br>

**Optimal Solution**
Consider the optimal alignment of $$X, Y$$ and its final position

There can be 3 relevant possibilities for the contents of the final position
  1. $$x_m, y_n$$ matched
  2. $$x_m$$ matched with a gap
  3. $$y_n$$ matched with a gap

> it is pointless to have 2 gaps (from $$X$$ and $$Y$$) matching because the penalty for gaps is non-negative, so if we just deleteed both of those gaps, we would get an event better alignment of $$X$$ and $$Y$$.

<br>

**Optimal Substructure**
Let $$X\prime = X - x_m, Y\prime = Y - y_n$$ (final characters of X and Y are removed)
As there are 3 optimal solutions
  1. case 1 holds, then induced alignment of $$X\prime$$ and $$Y\prime$$ is optimal
  2. case 2 holds, then induced alignment of $$X\prime$$ and $$Y$$ is optimal
  3. case 3 holds, then induced alignment of $$X$$ and $$Y\prime$$ is optimal

<br>

**The Recurrence**
$$P_{ij}$$ = penalty of optimal alignment of $$x_i$$ & $$y_j$$
for all i = 1,2,3,...,m and j = 1,2,3,...,n
  1. $$\alpha_{x_i y_j} + P_{(i-1)(j-1)}$$
  2. $$\alpha_{gap} + P_{(i-1),j}$$
  3. $$\alpha_{gap} + P_{i,(j-1)}$$

**The Algorithm**
> A = 2D array
> A[i,0] = A[0,i] = i * $$\alpha_{gap}\ \ \forall$$ i $$\geq$$ 0
>
> for i = 1 to m:
> - for j = 1 to n:
>   - A[i,j] = min ($$\alpha_{x_i y_j} + P_{(i-1)(j-1)}$$, $$\alpha_{gap} + P_{(i-1),j}$$, $$\alpha_{gap} + P_{i,(j-1)}$$)

<hr>
<br>

#### 03. Optimal Binary Search Tree
Optimal Cost Binary Search Tree, placing the most frequently used data in the root and closer to the root element, while placing the least frequently used data near leaves and in leaves.

Given a sorted array *keys[0,...,n-1]* of search keys and an array *freq[0,...,n-1]* of frequency counts, where *freq[i]* is the number of searches to *keys[i]*.

**Example**
> construct optimized binary search tree with least cost
> keys[ ] = {10, 20} and freq[ ] = {34, 50}
>
> Tree 1: 10 $$\rightarrow$$ 12
> Tree 2: 12 $$\rightarrow$$ 10
>
> Cost of a tree, C(T) = $$\Sigma_{i=0}\ freq(i) \times (depth(i) + 1)$$
> Cost of tree 1 is $$(34 \times 1) + (50 \times 2) = 134$$
> Cost of tree 2 is $$(50 \times 1) + (34 \times 2) = 118$$
>
> Therefore, Tree 2 is optimized binary search tree

<br>

Algorithm for finding optimal tree for sorted, distinct keys $$k_i...k_j$$
  - for each possible root $$k_r$$ for $$i \leq r \leq j$$
  - make optial subtree for $$k_i ... k_{r-1}$$
  - make optimal subtree for $$k_{r+1} ... k_j$$
  - select root that gives best total tree

Constraints
- as it is still Binary Search Tree, our solution must still satisfy one constaint that all child nodes in left side must be smaller than the root and all child nodes in right side must be greater than the root.

<br>

**Optimal Substructure**
Suppose an optimal BS for keys {1, 2,..., n} has root *r*, left subtree $$T_1$$, and right subtree $$T_2$$. $$T_1$$ is optimal for the keys {1, 2,.., r-1} and $$T_2$$ for the keys {r+1, r+2, ..., n}

$$$optCost(i,j) = \Sigma_{k=i}^{j}\ freq[k] + min_{r=i}^j[optCost(i, r-1) + optCost(r+1, j)]$$$

we one by one try all nodes as root (r varis from i to j in second term). When we make rth node as root, we recursively calculate optimal cost from i to r-1 and r+1 to j.

we add sum of frequencies from i to j (see first term in the above formula), this is added because every search will go through root and one comparison will be done for every search.

<br>

**Navie algorithm, exponential running time**
```java
// a naive recursive implementation of optimal
// binary search tree problem

public class Naive_Alg
{
    // a recursive function to calculate cost of
    // optimal binary search tree
    static int optCost(int freq[], int i, int j)
    {
        // base case
        if (j < i)        // no element in this subarray
            return 0;

        if (j == i)       // one element in this subarray
            return freq[i];


        // sum of freq[i], freq[i+1], ..., freq[j-1], freq[j]
        int fsum = sum(freq, i, j);

        // initialize minimum value
        int min = Integer.MAX_VALUE;

        // one by one consider all elements as root and
        // recursively find cost of the BST, compare the
        // cost with min and update min if needed
        for (int r=i; r<=j; ++r)
        {
            int cost = optCost(freq, i, r-1) + optCost(freq, r+1, j);

            if (cost < min)
                min = cost;
        }

        // return minimum value
        return min + fsum;
    }

    // a utility function to get sum of array element
    static int sum(int freq[], int i, int j)
    {
        int s = 0;
        for (int k = i; k <=j; k++)
            s += freq[k];
        return s;
    }

    // the main function that calculate minimum cost of
    // a Binary Search Tree. If mainly uses optCost() to
    // find the optimal cost.
    static int optimalSearchTree(int keys[], int freq[], int n)
    {
        // here array keys[] is assumed to be sorted in
        // increasing order. If keys[] is not sorted, then
        // add code to sort keys, and rearrange freq[]
        // accordingly.
        return optCost(freq, 0, n-1);
    }

    public static void main(String[] args)
    {
        int keys[] = {10, 12, 20};
        int freq[] = {34, 8, 50};
        int n = keys.length;

        System.out.println("Cost of Optimal BST is " +
                            optimalSearchTree(keys, freq, n));
    }
}
```

<br>

**Dynamic Programminng Algorithm for Optimal BST**
```java
// Dynamic Programming Java code for Optimal Binary Search
// Tree Problem

public class Optimal_BST
{
    // Dynamic Programming based function that calculates
    // minimum cost of a Binary Search Tree
    static int optimalSearchTree(int keys[], int freq[], int n)
    {
        // create an auxiliary 2D matrix to store results of
        // subproblems
        int cost[][] = new int[n + 1][n + 1];

        // cost[i][j] = Optimal cost of Binary Search Tree that
        // can be formed from key[i][j]. cost[0][n-1] will store
        // the resultant cost

        // for a single key, cost is equal to frequency of the key
        for (int i=0; i<n; i++)
            cost[i][i] = freq[i];

        // now we need to consider chains of length 2, 3, ... .
        // L is chain length
        for (int L=2; L<=n; L++)
        {
            // i is row number in cost[][]
            for (int i=0; i<=n-L+1; i++)
            {
                // get column number j from row number i and
                // chain length L
                int j = i + L - 1;
                cost[i][j] = Integer.MAX_VALUE;

                // try making all keys in interval keys[i..j] as root
                for (int r=i; r<=j; r++)
                {
                    // c = cost when keys[r] becomes root of this subtree
                    int c = ((r > i) ? cost[i][r - 1] : 0)
                            + ((r < j) ? cost[r + 1][j] : 0)
                            + sum(freq, i, j);

                    if (c < cost[i][j])
                        cost[i][j] = c;
                }
            }
        }

        return cost[0][n-1];
    }

    // a utility function to get sum of array element
    // freq[i] to freq[j]
    static int sum(int freq[], int i, int j)
    {
        int s = 0;
        for (int k=i; k<=j; k++)
        {
            if (k >= freq.length)
                continue;
            s += freq[k];
        }

        return s;
    }

    public static void main(String[] args)
    {
        int keys[] = {10, 12, 20};
        int freq[] = {34, 8, 50};
        int n = keys.length;

        System.out.println("Cost of Optimal BST is "
                + optimalSearchTree(keys, freq, n));
    }
}
```

> 1. Time complexity of the above solution is $$O(n^4)$$. The time complexity can be easily reduced to $$O(n^3)$$ by pre-calculating sum of frequencies instead of calling `sum()` again and again.
> 2. In the above solution, we have computed optimal cost only. The solution can be easily modified to store the structure of BSTs also. We can create another auxiliary array of size n to store the structure of tree. All we need to do is, store the chosen *'r'* in the innermost loop.