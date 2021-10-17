---
title:  "[Algorithm] Greedy algorithm"
date: 2021-10-13 1:8PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, codility]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-16 11:04AM
---

### What is greedy algorithm?
```text
1️⃣ We choose the best decision from the viewpoint of the current stage of the solution.

2️⃣ If it is not the best approach, then it often returns a result which is approximately correct but suboptimal.
```

---

### Tasks
#### `1. MaxNonoverlappingSegments` in codility (Lesson 16)
: Find a maximal set of non-overlapping segments


```java
class Solution { 
    public int solution(int[] A, int[] B) {
        
        int N = A.length;
        if (N == 0) return 0;

        int count = 1; // standard : skip A[0], B[0]
        int b_end = B[0];

        for (int i = 1; i < N; i++) {
            if (A[i] > b_end) {
                count++;
                b_end = B[i];
            }
        }

    } 
}
```

###### Question

```
Located on a line are N segments, numbered from 0 to N − 1, whose positions are given in arrays A and B. For each I (0 ≤ I < N) the position of segment I is from A[I] to B[I] (inclusive). The segments are sorted by their ends, which means that B[K] ≤ B[K + 1] for K such that 0 ≤ K < N − 1.

Two segments I and J, such that I ≠ J, are overlapping if they share at least one common point. In other words, A[I] ≤ A[J] ≤ B[I] or A[J] ≤ A[I] ≤ B[J].

For example, consider arrays A, B such that:
    A[0] = 1    B[0] = 5
    A[1] = 3    B[1] = 6
    A[2] = 7    B[2] = 8
    A[3] = 9    B[3] = 9
    A[4] = 9    B[4] = 10
The size of a non-overlapping set containing a maximal number of segments is 3. For example, possible sets are {0, 2, 3}, {0, 2, 4}, {1, 2, 3} or {1, 2, 4}. There is no non-overlapping set with four segments.

Write an efficient algorithm for the following assumptions:
    - N is an integer within the range [0..30,000];
    - each element of arrays A, B is an integer within - the range [0..1,000,000,000];
    - A[I] ≤ B[I], for each I (0 ≤ I < N);
    - B[K] ≤ B[K + 1], for each K (0 ≤ K < N − 1).
```

    
   
 
#### `2. TieRopes` in codility (Lesson 16)
: Tie adjacent ropes to achieve the maximum number of ropes of length >= K

```java
class Solution { 
    public int solution(int K, int[] A) {
        // return count when the sum is greater than or equals to K

        int count = 0;
        int sum = 0;

        for (int i = 0; i < A.length; i++) {
            sum += A[i];

            if (sum >= K) {
                count++;
                sum = 0;
            }
        }

        return count;
    } 
}
```


###### Question
```
There are N ropes numbered from 0 to N − 1, whose lengths are given in an array A, lying on the floor in a line. For each I (0 ≤ I < N), the length of rope I on the line is A[I].

We say that two ropes I and I + 1 are adjacent. Two adjacent ropes can be tied together with a knot, and the length of the tied rope is the sum of lengths of both ropes. The resulting new rope can then be tied again.

For a given integer K, the goal is to tie the ropes in such a way that the number of ropes whose length is greater than or equal to K is maximal.

For example, consider K = 4 and array A such that:
    A[0] = 1
    A[1] = 2
    A[2] = 3
    A[3] = 4
    A[4] = 1
    A[5] = 1
    A[6] = 3

We can tie:
- rope 1 with rope 2 to produce a rope of length A[1] + A[2] = 5;
- rope 4 with rope 5 with rope 6 to produce a rope of length A[4] + A[5] + A[6] = 5.

After that, there will be three ropes whose lengths are greater than or equal to K = 4. It is not possible to produce four such ropes.

For example, given K = 4 and array A such that:
    A[0] = 1
    A[1] = 2
    A[2] = 3
    A[3] = 4
    A[4] = 1
    A[5] = 1
    A[6] = 3
the function should return 3, as explained above.

Write an efficient algorithm for the following assumptions:
    - N is an integer within the range [1..100,000];
    - K is an integer within the range [1..1,000,000,000];
    - each element of array A is an integer within the range [1..1,000,000,000].
```

