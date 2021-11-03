---
title:  "[Algorithm] Binary search"
date: 2021-10-30 11:50AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-11-3 11:58PM
---

## 📌 **What is binary search algorithm?**
```text
1️⃣ Choose the middle element, as doing so causes the set of candidates to be halved each time.
(To reduce the set of candidates maximally.)

2️⃣ Use the information that all the elements are sorted

3️⃣ The time complexity is O(log n)
```

---

## 📌 **Implementation**
### - Java
- Iterative binary seach
: **More efficient** than recursive binary search

```java
// space complexity : O(1)
// time complexity : O(log n)

int BSearch(int arr[], int target) {
    int low = 0;
    int high = arr.length - 1;
    int mid;

    while (low <= high) {
        mid = (low + high) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] > target)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}
```
- Recursive binary search

```java

// space complexity : O(log N)
// time complexity : O(log n)

int BSearchRecursive(int arr[], int target, int low, int high) {
    
    if (low > high) return -1;

    int mid = (low + high) / 2;
    
    if (arr[mid] == target)
        return mid;
    else if (arr[mid] > target)
        return BSearchRecursive(arr, target, low, mid - 1);
    else
        return BSearchRecursive(arr, target, mid + 1, high);
}
```


The major difference between the **iterative** and **recursive version of Binary Search** is that the recursive version has a space complexity of **O(log N)** while the iterative version has a space complexity of **O(1)**. 
Hence, even though recursive version may be easy to implement, **the iterative version is efficient**.
Time complexity is same.

---

## 📌 **When is binary search best applied?**
Binary search is an efficient algorithm for **finding an item in an sorted array.**

---

## 📌 **Binary search tree vs Binary search**

### **- Binary search tree**
- A tree **data structure**
- Each node has up to 2 children 
- **The left subtree of a node** contains only nodes with keys **less than the node's key**
- **The right subtree of a node** contains only nodes with keys **greater than the node's key**

### **- Binary search**

- **An algorithm** that works on a **sorted** data structure (usually, but not necessarily, an array)
- At each step, looking at the value in the middle and **recursing to either the left or the right**, depending on **whether** the target value is **smaller or greater than the value in the middle** (or stopping if it's equal).

---

The source : <https://cjh5414.github.io/binary-search/> <br>

<https://stackoverflow.com/questions/21586085/difference-between-binary-search-and-binary-search-tree>