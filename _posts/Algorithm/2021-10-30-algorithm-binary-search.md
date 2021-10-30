---
title:  "[Algorithm] Binary search"
date: 2021-10-30 11:50AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-30 11:50AM
---

# **What is binary search algorithm?**
```text
1️⃣ Choose the middle element, as doing so causes the set of candidates to be halved each time.
(To reduce the set of candidates maximally.)

2️⃣ Use the information that all the elements are sorted

3️⃣ The time complexity is O(log n)
```
## 📌 Example
### - Java
- for loop
```java
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
- recursion
```java
int BSearchRecursive(int arr[], int target, int low, int high) {
    if (low > high)
        return -1;

    int mid = (low + high) / 2;
    if (arr[mid] == target)
        return mid;
    else if (arr[mid] > target)
        return BSearchRecursive(arr, target, low, mid-1);
    else
        return BSearchRecursive(arr, target, mid+1, high);
}
```

The source : <https://cjh5414.github.io/binary-search/>


### - Python
```python
def binarySearch(A, x): 
    n = len(A)
    beg=0
    end=n-1
    result = -1
    while (beg <= end):
        mid = (beg + end) / 2 
        if (A[mid] <= x):
            beg = mid + 1
            result = mid 
        else:
            end = mid - 1 
    return result
```
---