---
title:  "[Algorithm] Dynamic programming"
date: 2021-10-20 1:15AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, codility]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-20 1:35AM
---

I've mentioned this before, but I'm gonna explain it in more detail.

---
# **What is dynamic programming?**

```text
An algorithmic paradigm that
1️⃣ solves a given complex problem by breaking it into subproblems
and
2️⃣ stores the results of subproblems to avoid computing the same results again
```
---

# **Feature of dynamic programming**

## 📌 Memoization

1. make dynamic table and **store the results** of expensive function calls for do later things.

2. When you do the next task, **you calculate it by looking at the values stored in the table,** it's not calculating it from the beginning. 


## 📌 Condition (Property)

For dynamic programming, these two conditions is needed.

1. Optimal substructure
    : - An optimal solution to the problem contains an optimal solution to subproblems.

2. Overlapping problems
    : - A problem have overlapping **subproblems which are reused several times or a recursive algorithm** for the problem **solves the same subproblem** over and over rather than always generating new subproblems.


## 📌 Example
- Assembly Line Problem
- Matrix Chain Multiplication Problem
- 0/1 Knapsack Problem 


---
## **⭐️ Plus**
### **'Dynamic programming' 🆚 'Divide and conquer algorithm'**

1. Common feature
```
solve an optimization problem 
by breaking it down into simpler subproblem
```

2. Difference

 **the divide and conquer**
    : **combines the solutions of the sub-problems** to obtain the solution of the main problem 

**dynamic programming**
    : **uses the result of the sub-problems** to find the optimum solution of the main problem

