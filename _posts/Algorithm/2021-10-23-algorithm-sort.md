---
title:  "[Algorithm] Sort"
date: 2021-10-23 7:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-23 7:30PM
---
# Sort
---

# Task
# 1. 가장 큰 수 in Programmers (Level 2)
## 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42746>

## 📌 The point
- Used **Arrays.sort(array, Comparator<E>)**
    - It's one of the **fast** way to sort array

    - **[Different type 1]**

        ```java
        Arrays.sort(array)
        ```

        - If array is primitive type such as int[] and char[], it use **Dual-Pivot QuickSort** (InsertionSort + QuickSort).
        - If array is Object type such as String[] and Integer[], it use **TimSort** (InsertionSort + MergeSort).

    --


    - **[Different type 2]**  
        ```java
        Arrays.sort(array, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return ((o2 + o1).compareTo(o1 + o2));
        });
        ```

## 📌 Answer
```java
import java.util.Arrays;

class Solution {

	public String solution(int[] numbers) {

		// Convert int array to String array
		String[] result = new String[numbers.length];
		for (int i = 0; i < numbers.length; i++)
			result[i] = String.valueOf(numbers[i]);
		

		// Sort (lambda expression)
        // specific meaning : String.compareTo(String)
        // why (o2 + o1)? because it sort datas by dscending order
        // then, (o1 + o2) -> become ascending order
		Arrays.sort(result, (o1, o2) -> (o2 + o1).compareTo(o1 + o2));
                // [Same expression]
                // Comparator<String> comp = (o1, o2) -> (o2 + o1).compareTo(o1 + o2);
                // Arrays.sort(result, comp);

		
                // If there are multiple zero, return only 0
		if (result[0].equals("0")) {
			return "0";
		}

        // Convert String array to String
		String answer = "";
		for (String a : result) answer += a;

		return answer;
	}
}
```
The source : <https://haeng-on.tistory.com/7>

Don't forget the contents of OCPJP!
It's quite useful on coding test.