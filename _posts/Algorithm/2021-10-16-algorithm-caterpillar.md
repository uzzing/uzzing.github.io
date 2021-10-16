---
title:  "[Algorithm] Caterpillar method"
date: 2021-10-16 7:31PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-16 7:31PM
---

## What is caterpillar method?
```text
1️⃣ The idea is to check elements in a way that’s reminiscent of movements of a caterpillar.

2️⃣ The caterpillar crawls through the array. We remember the front and back positions of the caterpillar, and at every step either of them is moved forward.
```

---

## Tasks
#### `1. AbsDistinct ` in codility (Lesson 15)
: Compute number of distinct absolute values of sorted array elements

#### ⭐️ `The point`
- Math.abs(number) ➡️ import java.lang.Math;
- HashSet ➡️ import java.util.HashSet; / import java.util.Set; 

```java
import java.lang.Math;
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int solution(int[] A) {

        Set<Integer> set = new HashSet<>();

        for (int i : A)
            set.add(Math.abs(i));

        return set.size();
    }
}
```

#### ⭐️ `Review`
##### Set : no sequence, no duplicate
| **class** | features | method |
|:---:|:---:|:---:|
|**HashSet**|	순서가 필요없는 데이터를 hash table에 저장. Set 중에 가장 성능이 좋음| add(), size(), equals(), hashCode(), removeAll() |
|**TreeSet**|	저장된 데이터의 값에 따라 정렬됨. red-black tree 타입으로 값이 저장. HashSet보다 성능이 느림|
|**LinkedHashSet**|	연결된 목록 타입으로 구현된 hash table에 데이터 저장. 저장된 순서에 따라 값이 정렬. 셋 중 가장 느림|

#### `Question`

```
given a non-empty array A consisting of N numbers, returns absolute distinct count of array A.

For example, consider array A such that:
  A[0] = -5
  A[1] = -3
  A[2] = -1
  A[3] =  0
  A[4] =  3
  A[5] =  6
The absolute distinct count of this array is 5, because there are 5 distinct absolute values among the elements of this array, namely 0, 1, 3, 5 and 6.

Write an efficient algorithm for the following assumptions:
    - N is an integer within the range [1..100,000];
    - each element of array A is an integer within the range [−2,147,483,648..2,147,483,647];
    - array A is sorted in non-decreasing order.
```

--- 
 
#### `2. CountDistinctSlices` in codility (Lesson 15)
: Count the number of distinct slices (containing only unique numbers)

It's quite difficult.....
#### ⭐️ `The point`
- boolean[] ➡️ to check which value is already checked.
- divide case  ➡️ case1. distinct, case2. not distinct

```java
class Solution {
    public int solution(int M, int[] A) {

        boolean[] seen = new boolean[M+1]; // 0~M

        // pair (p, q)
        int p = 0;
        int q = 0;
        int count = 0;

        // move p and q
        while (p < A.length && q < A.length) {

            // case1. not distinct
            if (seen[A[q]] == true) {
                seen[A[p]] = false;
                p++; // go to next
            }
            else { // case2. distinct
                seen[A[q]] = true;
                count += (q - p + 1); // not just 'count++;', it has to be 
                q++;
            }

            if (count > 1000_000_000) return 1000_000_000;

        }
        return count;
    }
}

```


#### `Question`
```
Given an integer M and a non-empty array A consisting of N integers, returns the number of distinct slices.

A pair of integers (P, Q), such that 0 ≤ P ≤ Q < N, is called a slice of array A. 
The slice consists of the elements A[P], A[P + 1], ..., A[Q]. 
A distinct slice is a slice consisting of only unique numbers. 
That is, no individual number occurs more than once in the slice.

For example, consider integer M = 6 and array A such that:
    A[0] = 3
    A[1] = 4
    A[2] = 5
    A[3] = 5
    A[4] = 2
There are exactly nine distinct slices:
 (0, 0), (0, 1), (0, 2), (1, 1), (1, 2), (2, 2), (3, 3), (3, 4) and (4, 4).

Write an efficient algorithm for the following assumptions:
    - N is an integer within the range [1..100,000];
    - M is an integer within the range [0..100,000];
    - each element of array A is an integer within the range [0..M].
```

--- 

#### `3. CountTriangles` in codility (Lesson 15)
: Count the number of triangles that can be built from a given set of edges.


```java
class Solution {
    public int solution(int[] A) {

        
    }
}
```


#### `Question`
```

```



---
### `New words`


reminiscent 連想させる
contiguous 連続的な
subsequence 次
compute 計算する
distinct absolute values 絶対値