# Unit_3_assignment_DAA_AshmitShekhar
# DAA Assignment (GGSIPU 5th Sem BTech CSE)

> Solutions for: SECTION A – Short Theory & SECTION B – Algorithms & Recurrences

---

## SECTION A – Short Theory [15 Marks]

### DP essentials
**Three ingredients of Dynamic Programming (one-line purpose each):**
1. **Optimal substructure** — a problem's optimal solution can be constructed from optimal solutions of its subproblems.
2. **Overlapping subproblems** — subproblems recur many times so their results can be reused.
3. **State & choice (DP formulation)** — a precise definition of state and choice to build recurrence and compute solutions.

### DP vs Divide & Conquer (two differences + example each)
1. **Subproblem overlap:** DP requires overlapping subproblems (reuse results); D&C splits into independent subproblems (no reuse).  
   *Example DP:* Fibonacci with memoization.  
   *Example D&C:* Merge Sort (subproblems independent).
2. **Reuse of solutions:** DP stores and reuses subproblem results (memo/tabulation); D&C recomputes or combines without storing intermediate results.  
   *Example DP:* Matrix Chain Multiplication (stores m[i,j]).  
   *Example D&C:* Quick Sort partitioning.

### Principle of optimality
**Definition (one sentence):** If an optimal solution to a problem contains within it optimal solutions to subproblems, the problem satisfies the principle of optimality.  
**Example of a problem that satisfies it:** Shortest path (single-source shortest path in a graph without negative cycles), or Matrix Chain Multiplication.

### Memoization (one-line each)
**Memoization:** Top-down DP where computed subproblem results are stored (cached) and reused when the same subproblem recurs.  
**Tabulation:** Bottom-up DP where results are computed iteratively in an order that ensures dependencies are already computed (no recursion).

### Branch and Bound idea (two lines)
**Branch-and-Bound (BnB):** Systematic search that branches on decision choices and maintains bounds (upper/lower) on the best possible solution in each branch.  
**Role of bounding:** The bounding function estimates the best achievable value inside a branch; if the bound indicates the branch cannot beat the current best solution, the branch is pruned (discarded).

---

## SECTION B – Algorithms & Recurrences [15 Marks]

### 1) Matrix Chain Multiplication
Given matrices: A₁: 5×4, A₂: 4×6, A₃: 6×2, A₄: 2×7 (so dimensions p = [5,4,6,2,7])

**(a) Recurrence and base case**
- Base case: \(m[i,i]=0\) for all i.  
- Recurrence: \(m[i,j]=\min_{i\le k<j}\{\,m[i,k]+m[k+1,j]+p_{i-1}\cdot p_k\cdot p_j\,\}\).

**(b) Minimum scalar multiplications**
- **Answer:** `158` scalar multiplications.

*(Computed by standard DP for matrix chain.)*

---

### 2) Longest Common Subsequence (LCS)
Strings: X = "ABCDGH", Y = "AEDFHR"

**(a) Recurrence and base**
- Base: \(\text{LCS}(i,0)=0,\;\text{LCS}(0,j)=0\).  
- Recurrence:
  - If \(X[i]==Y[j]\) then \(\text{LCS}(i,j)=\text{LCS}(i-1,j-1)+1\).  
  - Else \(\text{LCS}(i,j)=\max(\text{LCS}(i-1,j),\text{LCS}(i,j-1))\).

**(b) LCS length (number only):** `3`

---

### 3) Optimal Binary Search Tree (OBST)
Keys: 10, 20, 30 with probabilities \(p_1=0.4, p_2=0.3, p_3=0.3\). Assume \(q_i=0\) (no dummy keys).

**(a) DP formulations (w and e) with base**
- Weight sum: \(w[i,j]=\sum_{t=i}^{j} p_t\).  
- Expected cost DP: \(e[i,j]=\min_{r=i}^j\{ e[i,r-1] + e[r+1,j] + w[i,j] \}\).  
- Base: \(e[i,i-1]=0,\; w[i,i-1]=0\) for all i.

**(b) Minimum expected search cost (number only):** `1.7`

---

### 4) 0/1 Knapsack – Branch & Bound
Capacity \(W=5\). Items (indices 1..4):
- weights: \(w = [2,3,4,5]\)
- profits: \(p = [3,4,5,6]\)

**(a) Fractional upper-bound formula used for pruning**

Let items be ordered by nonincreasing profit/weight ratio. For a partial node with current value \(v\), current weight \(W_c\), and remaining capacity \(R = W - W_c\), the fractional upper bound is:

\[
\text{ub} = v + \sum_{i\in\text{remaining, in ratio order}} p_i \cdot x_i
\]

where each \(x_i\) = 1 if \(w_i \le R\) (take whole item), else \(x_i = R / w_i\) for the first item that doesn't fit (fractional part), and then stop.

(Short-form formula frequently written as) \(\text{ub} = v + \text{fractional\_fill}(R)\).

**(b) Show level-0 and level-1 nodes (include/exclude first item) with (v,w,ub) only**
- Items' profit/weight ratios: item1: 3/2 = 1.5, item2: 4/3 ≈ 1.333, item3: 5/4 = 1.25, item4: 6/5 = 1.2 — already in decreasing order.

- **Level-0 (root):** include nothing yet → \((v=0, w=0, \; ub=7)\).  
  Explanation: fractional fill by items 1 & 2 exactly fits capacity (2+3=5) giving ub = 3+4 = 7.

- **Level-1 (include first item):** include item1 → \((v=3, w=2, \; ub=7)\).  
  Explanation: after including item1 (v=3,w=2) remaining capacity 3 can take item2 fully (profit 4) so ub = 3+4 = 7.

- **Level-1 (exclude first item):** exclude item1 → \((v=0, w=0, \; ub=6.5)\).  
  Explanation: best fractional fill without item1 is item2 (w3,p4) plus half of item3 (0.5×5=2.5) → ub = 4 + 2.5 = 6.5.

---

### 5) TSP – Dynamic Programming (Held–Karp)
(Assume cities numbered 1..4 and city 1 is the start/end; the user mentioned an example distance matrix D but did not provide its numeric values.)

**(a) Recurrence and final expression**
- Recurrence for subset S (subset of \{2..n\}) and endpoint \(j\in S\):
  \[
  C[S,j] = \min_{i\in S\setminus\{j\}} \{ C[S\setminus\{j\}, i] + d(i,j) \}
  \]
- Final answer (minimum tour cost):
  \[
  \min_{j\in\{2..n\}} \{ C[\{2..n\}, j] + d(j,1) \}\n
  \]
- Base case: \(C[\{k\}, k] = d(1,k)\) for k = 2..n.

**(b) Initialize base entries \(C[\{k\},k]\) for k=2..4 (numbers only)**

I cannot give numeric values for these base entries because the distance matrix **D** (the values \(d(1,2), d(1,3), d(1,4)\)) was not provided in the problem statement.  

**Format/example if D were given:**
```
C[{2},2] = d(1,2)
C[{3},3] = d(1,3)
C[{4},4] = d(1,4)
```
(Replace `d(1,k)` by the numeric distances from city 1 to k when D is available.)

---

### Notes & References
- Numeric answers (Matrix Chain = 158, LCS length = 3, OBST cost = 1.7) were computed using standard DP algorithms.

---



