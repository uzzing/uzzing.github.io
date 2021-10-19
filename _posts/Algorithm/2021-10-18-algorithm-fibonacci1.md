---
title:  "[Algorithm] Fibonacci numbers1"
date: 2021-10-18 10:35PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, codility]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-19 9:19PM
---

## What is fibonacci numbers?

```text
1️⃣ The first two numbers in the Fibonacci sequence are 0 and 1, 
and each subsequent number is the sum of the previous two.

2️⃣ Enumeration of the Fibonacci numbers can be done faster simply 
by using a basis of dynamic programming
```

![fibonacci numbers](https://user-images.githubusercontent.com/83699657/137673772-b993cd72-59f9-4532-a5ea-a2f85c3c6295.jpg)

###`Example not efficient`
Finding Fibonacci numbers recursively.
```python
def fibonacci(n): 
    if (n <= 1): 
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```
###**`Example efficient`**
Finding Fibonacci numbers **dynamically. 
(by using a basis of dynamic programming)**

The time complexity of this algorithm is **O(n)**.
```python
def fibonacciDynamic(n):
    fib = [0] * (n + 2) # initialization
    fib[1] = 1 # fib[0] = 0
    for i in xrange(2, n + 1): # memozation
        fib[i] = fib[i - 1] + fib[i - 2]
    return fib[n]
```
---
### + Then, what is dynamic programming?
```
1️⃣ An algorithmic technique for solving an optimization problem 
by breaking it down into simpler subproblem

2️⃣ Store the result of subproblems and reuse it
```
#### `The point`
#####`⭐️ Memoization `
: **store the results** of expensive function calls and returning the cached result when the same inputs occur again.


#####**`⭐️ VS 'Divide and conquer algorithm'`**
- **`Common feature`**
```
solve an optimization problem 
by breaking it down into simpler subproblem
```


- **`Difference`**
```
the divide and conquer 
: combines the solutions of the sub-problems to obtain the solution of the main problem 

dynamic programming
: uses the result of the sub-problems to find the optimum solution of the main problem
```

---

## Tasks
### `1. FibFrog ` in codility (Lesson 13)
: Count the minimum number of jumps required for a frog to get to the other side of a river.

It's quite difficult lol🥲


#### `Question`
https://app.codility.com/programmers/lessons/13-fibonacci_numbers/fib_frog/


#### `Answer`
[RESULT](https://app.codility.com/demo/results/trainingTYPCBS-MK8/)
```java
class Solution {

    private int[] fibArray;

    public int solution(int[] A) {
        
        int N = A.length;
        makeFibArray(N);

        int fibLength = fibArray.length;

        int result = -1;

        for (int i = 0; i <= N; i++) { // i : for A array

            if (i == N || A[i] == 1) {
                int min = Integer.MAX_VALUE;

                for (int j = 0; j < fibLength && fibArray[j] <= i + 1; j++) { // j : for fibArray
                    
                    final int start = i - fibArray[j];

                    if (start == -1) min = 1;
                    else if (A[start] > 0) {
                        if (A[start] + 1 < min) min = A[start] + 1;
                    }
                }

                if (i < N) {
                    if (min == Integer.MAX_VALUE) A[i] = 0;
                    else                        A[i] = min;
                }
                else { // i == N : arrived
                    if (min != Integer.MAX_VALUE) result = min;
                }
            }
        }
        return result;

    }

    private void makeFibArray(int N) {
        fibArray = new int[N < 2 ? 2 : N + 1]; 
        fibArray[0] = 1;
        fibArray[1] = 2;
        
        for (int i = 2; fibArray[i - 1] <= N; i++)
            fibArray[i] = fibArray[i - 1] + fibArray[i - 2];
    }
}
```