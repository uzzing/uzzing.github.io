---
title:  "[Algorithm] Big-O notation"
date: 2021-11-3 1:58PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-11-3 1:58PM
---

# Big-O notation
## 📌 What is it?
- a mathematical notation that describes **the limiting behavior of a function** when the argument tends towards a particular value or infinity.

- In computer science, big O notation is used to classify algorithms according to **how their run time or space requirements grow** as the input size grows.

- **`Time complexity + Space complexity`**

---
## 📌 Let's compare
**O(1) < O(log n) < O(n) < O(n * log n) < O(n²) < O(n³) < O(2^n) < O(n!)**

And,
Big-O notation ignores the following case
- O(2N) -> O(N)
- O(N² + 2) > O(N²)
- O(N² + N) -> O(N²)

![big-o](https://user-images.githubusercontent.com/83699657/140009538-43f388e4-164f-42a4-9721-509e1ac7dd96.png)

---
## 📌 Example
### Time complexity
```java
// O(1)
int sum1(int N) {
    return N * N;
}

// O(2N) => O(N)
int sum2(int N) {
    sum = 0;

    for (int i = 1; i <= N; i++) {
        sum = sum + N;
    }    

    return sum;
}

// O(N²)
int sum3(int N) {
    sum = 0;

    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= N; j++) {
            sum = sum + 1;
        }
    }

    return sum;
}
```

### Space complexity
```java
//  O(N)
// recursion
int sum(int N) {
    sum = 0;
    if (N < 1)
        return 0;
    return N + sum(N - 1);
}

// O(1)
int mainSum(int N) {
    int result = 0;

    for (int i = 0; i < N; i++)
        result += sum(i, i + 1);

    return result;
}

int sum(int a, int b) {
    return a + b;
}
```

---
## 📌 Time complexity 
### Binary search
**`O(logN)`**

#### Example1. Find the square root (√)

<img width="172" alt="Screen Shot 2021-11-03 at 1 49 45 PM" src="https://user-images.githubusercontent.com/83699657/140011286-29684557-56bc-4435-8d0b-6c971f4f082f.png">


<img width="573" alt="Screen Shot 2021-11-03 at 1 51 24 PM" src="https://user-images.githubusercontent.com/83699657/140011380-8197aee5-88ee-428c-b7fc-54f5d6905dff.png">


```java
// O(logN)
public static int squareRootBSearch(int n) {
    int min = 0;
    int max = n;
    int guess;

    while (min <= max) {
        guess = (min + max) / 2;
        if (guess * guess == n)
            return guess;
        else if (guess * guess > n)
            max = guess - 1;
        else
            min = guess + 1;
    }

    return -1;
}

// not binary search
// O(N)
public static int squareRootLoop(int n) {
    for (int i = 0; i < n; i++)
        if (i * i == n)
            return i;
    return -1;
}
```

--- 
### Sorting algorithm

- Efficient but not simple algorithm
    - quick sort(1), heap sort(3), merge sort(2)

![sort](https://user-images.githubusercontent.com/83699657/140009614-5c8daeff-e292-474d-9e37-9cb24dd57c67.png)


---
The source : <br>
<https://cjh5414.github.io/big-o-notation/> <br>
<https://cjh5414.github.io/binary-search/> <br>
<https://velog.io/@gillog/시간복잡도> <br>
<https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html>