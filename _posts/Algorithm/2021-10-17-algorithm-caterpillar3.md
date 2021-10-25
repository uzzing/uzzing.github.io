---
title:  "[Algorithm] Caterpillar method 3"
date: 2021-10-17 12:08PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Codility]
tags: [algorithm, java, eng, codility]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-17 12:08PM
---
[See previous post](https://uzzing.github.io/posts/algorithm-caterpillar2/)

## Tasks
### `4. MinAbsSumOfTwo` in codility (Lesson 15)
: Find the minimal absolute value of a sum of two elements.

**`My first answer`** 
- It occurred timeout error...
- Time complexity: O(N * N) (No~~~~~😫)

```java
import java.lang.Math;

class Solution {
    // (P, Q)  ->  |A[P] + A[Q]|, 0 ≤ P ≤ Q < N
    // 1. set a -> for
    // 2. set b -> for ** I wondered multiple for loop is okay for time complexity?
    // 3. get a + b and make it to the absolute value 
    // 4. compare the previous value -> if the current is smaller, save to variable
    // 5. return the last value
    private int min = 0;

    public int solution(int[] A) {
        min = Math.abs(A[0] + A[0]);

        for (int a : A) {
            for (int b : A) {
                if (min > Math.abs(a + b)) min = Math.abs(a + b);
            }
        }
        return min;
    }
}
```
---

#### **`Final answer`** 
#### ⭐️ `The point`
- **Don't use only for loop** 
-> I thought two for loop is okay lol
-> Let's avoid two for loop, too!!
- **Don't forget this problem is related with caterpillar method algorithm**

[RESULT](https://app.codility.com/demo/results/trainingGYFDTC-X7D/)

```java
import java.util.Arrays;
import java.lang.Math;

class Solution {
    public int solution(int[] A) {
       int min = Integer.MAX_VALUE;
       int p = 0;
       int q = A.length - 1;

       Arrays.sort(A);

       while (p <= q) { // the other way of for loop
            int current = A[p] + A[q];
            min = Math.min(min, Math.abs(current));
            
            // caterpillar method
            if (current < 0) p++; // -
            else q--; // +
       }
    
        return min;
    }
}
```

#### `Question`
```
Let A be a non-empty array consisting of N integers.
The abs sum of two for a pair of indices (P, Q) is the absolute value |A[P] + A[Q]|, for 0 ≤ P ≤ Q < N.

For example, the following array A:
  A[0] =  1
  A[1] =  4
  A[2] = -3
has pairs of indices (0, 0), (0, 1), (0, 2), (1, 1), (1, 2), (2, 2). 
The abs sum of two for the pair (0, 0) is A[0] + A[0] = |1 + 1| = 2. 
The abs sum of two for the pair (0, 1) is A[0] + A[1] = |1 + 4| = 5. 
The abs sum of two for the pair (0, 2) is A[0] + A[2] = |1 + (−3)| = 2. 
The abs sum of two for the pair (1, 1) is A[1] + A[1] = |4 + 4| = 8. 
The abs sum of two for the pair (1, 2) is A[1] + A[2] = |4 + (−3)| = 1. 
The abs sum of two for the pair (2, 2) is A[2] + A[2] = |(−3) + (−3)| = 6.

the function should return 1, as explained above.

Write an efficient algorithm for the following assumptions:
    - N is an integer within the range [1..100,000];
    - each element of array A is an integer within the range [−1,000,000,000..1,000,000,000].
```

---
### `New words`
- indices : multiple indexes
