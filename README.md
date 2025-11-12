# Unit III – Assignment  

Name: Ashmit Shekhar  
Enrollment no: 07713302723

## SECTION A – Short Theory [15 Marks]

1) DP essentials  
- List the three ingredients of DP and one-line purpose of each. 
  
   Ans:  - Optimal Substructure: Optimal solution is built from optimal solutions of subproblems.  
         - Overlapping Subproblems: Same subproblems repeat; solve once and reuse.  
         - State & Transition: Define DP state and recurrence to compute and store results efficiently.  

---
2) DP vs D&C  
- State two differences focusing on subproblem overlap and reuse; give one example for each. 

    Ans: DP: Overlapping subproblems and results reused using memoization/tabulation.  
             Example: Fibonacci using DP.  
        - Divide & Conquer:Subproblems independent; recomputation occurs.  
             Example: Merge Sort.  

---
3) Principle of optimality  
- Define it in one sentence and name any one problem satisfying it.
Ans- Definition: If an optimal solution contains optimal solutions to its subproblems, the problem follows the principle of optimality.  
- Example: Matrix Chain Multiplication.  

---

 4. Memoization  
Define memoization and contrast with tabulation in one line each.

Ans- Memoization:Top-down approach storing results of solved subproblems to avoid recomputation.  
- Tabulation: Bottom-up approach computing all subproblems iteratively in a table.  

---

5. Branch and Bound Idea  
Define BnB and the role of bounding in pruning in two lines.

Ans- Definition: A state-space search method that generates branches of partial solutions while tracking bounds of optimal value.  
- Bounding: Bound estimates the best achievable value from a node; weak nodes are pruned to reduce search.  

---
SECTION B – Algorithms & Recurrences (15 Marks)

### 6. Matrix Chain Multiplication (A₁:5×4, A₂:4×6, A₃:6×2, A₄:2×7)

**a)** Recurrence and base case:
```text
m[i,i] = 0
m[i,j] = min for i ≤ k < j { m[i,k] + m[k+1,j] + p[i-1] * p[k] * p[j] }

b) Minimum scalar multiplications (number only):
158
---

7. Longest Common Subsequence (X = "ABCDGH", Y = "AEDFHR")

a) Recurrence and base case:

LCS(i,0) = 0, LCS(0,j) = 0
if X[i] == Y[j]:
    LCS(i,j) = LCS(i-1, j-1) + 1
else:
    LCS(i,j) = max( LCS(i-1,j), LCS(i, j-1) )


b) LCS length (number only):
3
---

8. Optimal Binary Search Tree

(keys: 10,20,30; p = 0.4,0.3,0.3; assume q = 0)

a) DP formulation with base:

e[i,i-1] = 0;  w[i,i-1] = 0
w[i,j] = w[i, j-1] + p[j]
e[i,j] = min for r = i..j { e[i,r-1] + e[r+1,j] + w[i,j] }


b) Minimum expected search cost (number only):
1.7
---

9. 0/1 Knapsack – Branch & Bound

(W = 5; w = {2,3,4,5}, p = {3,4,5,6})

a) Fractional upper bound formula:

ub = V + sum of next items fully fitting + (fraction of next item if partially fits)


b) Level-0 and Level-1 nodes (v, w, ub):

Level-0 (Root): (0, 0, 7.0)

Level-1 Include Item1: (3, 2, 7.0)

Level-1 Exclude Item1: (0, 0, 6.5)
---

10. TSP – Dynamic Programming (Held–Karp; 4 cities)

a) Recurrence and final expression:

C[{k},k] = D[1][k]
C[S,j] = min for i ∈ S, i ≠ j { C[S-{j},i] + D[i][j] }
Final = min for j ∈ {2..n} { C[{2..n},j] + D[j][1] }


b) Base entries C[{k},k] for k = 2..4:
C[{2},2] = D[1,2]
C[{3},3] = D[1,3]
C[{4},4] = D[1,4]
