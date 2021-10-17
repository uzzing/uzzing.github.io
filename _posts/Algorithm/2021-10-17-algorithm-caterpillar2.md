---
title:  "[Algorithm] Caterpillar method 2"
date: 2021-10-17 11:02PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, codility]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-17 11:02PM
---
[See previous post](https://uzzing.github.io/posts/algorithm-caterpillar/)
## Tasks
### `3. CountTriangles` in codility (Lesson 15)
: Count the number of triangles that can be built from a given set of edges.


**`My first answer`** -> occurred timeout errors....
- Time complexity : O(N**3) 
- Performance tests : score 0 
...🥲

The reason why it occured errors : nested loop (I guess) 
-> so answer can't be tested with large datas

```java
class Solution {
    public int solution(int[] A) {
        // p, q, r -> A[P], A[Q] and A[R], 0 ≤ P < Q < R < N
        // 1. set p -> for
        // 2. set q -> for
        // 3. set r -> for
        // 4. check conditions
        //      A[P] + A[Q] > A[R] : 1 + 2 > 3 -> if
        //      A[Q] + A[R] > A[P] : 2 + 3 > 1 -> if
        //      A[R] + A[P] > A[Q] : 3 + 1 > 2 -> if
        //      count++
        //      else continue;

        int count = 0;

        for (int p = 0; p < A.length - 2; p++) { // p
            for (int q = p + 1; q < A.length - 1; q++) { // q
                for (int r = q + 1; r < A.length; r++) { // r
                    if (A[p] + A[q] > A[r])
                        if (A[q] + A[r] > A[p])
                            if (A[r] + A[p] > A[q]) count++;
                    else continue;
                }
            }
        }
        return count;
    }
}
```

So,,,what should I do to solve it more efficiently?
#### ⭐️ `The point`
- **Don't use only for loop** -> There are many other ways instead of for loop
- In addition, let's start considering abstraction when you write code

[RESULT](https://app.codility.com/demo/results/trainingBTG536-3G3/)

```java
import java.util.Arrays;

class Solution {
    
    // Encapsulation
    private int count = 0;
    private int[] A;

    public int solution(int[] A) {
        this.A = A;
        Arrays.sort(this.A);

        for (int p = 0; p < A.length - 2; p++) {

            int q = p + 1;
            int r = q + 1;

            while (q < A.length - 1) {
                if (r < A.length && isTriangular(p, q, r)) {
                    r++;
                } else {
                    count += (r - q - 1); // important
                    q++;
                }
            }
        }

        return count;
    }

    // abstraction
    private boolean isTriangular(int p, int q, int r) {
        return A[p] + A[q] > A[r] && A[q] + A[r] > A[p] && A[r] + A[p] > A[q];
    }
}
```

#### `Question`
```
An array A consisting of N integers is given. A triplet (P, Q, R) is triangular if it is possible to build a triangle with sides of lengths A[P], A[Q] and A[R]. In other words, triplet (P, Q, R) is triangular if 0 ≤ P < Q < R < N and:

A[P] + A[Q] > A[R],
A[Q] + A[R] > A[P],
A[R] + A[P] > A[Q].

For example, consider array A such that:
  A[0] = 10    A[1] = 2    A[2] = 5
  A[3] = 1     A[4] = 8    A[5] = 12
There are four triangular triplets that can be constructed from elements of this array, 
namely (0, 2, 4), (0, 2, 5), (0, 4, 5), and (2, 4, 5).
the function should return 4, as explained above.

Write an efficient algorithm for the following assumptions:
    - N is an integer within the range [0..1,000];
    - each element of array A is an integer within the range [1..1,000,000,000].
```

---
### `New words`
- triplets 三つ構成のセット
