---
title:  "[Data Sturcture] Quick sort"
date: 2021-10-19 1:31PM
excerpt: "coding test"

author: Yuha
categories: [Development, DataStructure]
tags: [datastructure, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-19 1:31PM
---

## What is quick sort?

```text
Make a pivot which means middle index to divide array.
It is based on divide and conquer algorithm 
```

![quick-sort](https://user-images.githubusercontent.com/83699657/137864838-bf636663-6bb8-483d-ab35-1272f7cfa7b4.png)

---

###**`Implementation`**
####`⭐️ The point`
- quickSort() : main
- sort()
- partition()
- swap()

```java
public class QuickSorter {

    // main
    public static void quickSort(int[] arr) {
        sort(arr, 0, arr.length - 1);
    }

    private static void sort(int[] arr, int low, int high) {
        if (low >= high) return;

        int mid = partition(arr, low, high); // divide
        sort(arr, low, mid - 1); // 0 ~ mid - 1
        sort(arr, mid, high); // mid ~ arr.length - 1
    }

    private static int partition(int[] arr, int low, int high) {
        
        int pivot = arr[(low + high) / 2];
        
        while (low <= high) {
            while (arr[low] < pivot) low++;
            while (arr[high] > pivot) high--;
            if (low <= high) {
                swap(arr, low, high);
                low++;
                high--;
            }
        }

        return low;
    }

    private static void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
}
```