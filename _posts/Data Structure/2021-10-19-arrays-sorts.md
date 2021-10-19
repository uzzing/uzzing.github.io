---
title:  "[Data Sturcture] Arrays.sort() (+ with lambda)"
date: 2021-10-19 1:31PM
excerpt: "coding test"

author: Yuha
categories: [Development, DataStructure]
tags: [datastructure, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-19 1:31PM
---

## What is ###.sort()?

```text
1️⃣ sort the datas of array or list ascending order or descending order
```
## Sort array
### `Arrays.sort()`
the primitive way to sort **array** until Java7
```java
// Ascending order
int[] array = new int[] {2, -1, 9, 4};
Arrays.sort(array);
System.out.prinln(array); // {-1, 1, 4, 9};

// Descending order
// *** Only wrapper class can be sorted by descending order 
Integer[] array = new Integer[] {2, -1, 9, 4};
Arrays.sort(array, Collections.reverseOrder());
System.out.prinln(array); // {9, 4, 2, -1};

// lambda expression
Arrays.sort(array, (int x[] - int y[] -> x[0] - y[0]))
```

## Sort list
### **`1. Collections.sort()`**

the way to sort **list** until Java7

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections; // important

public class Sort {
    public static void main(String[] args) {

        ArrayList<String> list = new ArrayList<>(Arrays.asList("C", "A", "B", "a"));

        // Ascending order
        Collections.sort(list);
        System.out.println(list); // [A, B, C, a]

        // Descending order
        Collections.sort(list, Collections.reverseOrder());
        System.out.println(list); // [a, C, B, A]

        // Ascending order without checking cases (uppercase and lowercase)
        Collections.sort(list, String.CASE_INSENSITIVE_ORDER);
        System.out.println(list); // [a, A, B, C]

        // Descending order without considering cases (uppercase and lowercase)
        Collections.sort(list, Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER));
        System.out.println(list); // [C, B, a, A]
    }
}
```

### **`2. List.sort()`**

the ways to sort **list** from Java8

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator; // important

public class Sort {
    public static void main(String[] args) {
        
        ArrayList<String> list = new ArrayList<>(Arrays.asList("C", "A", "B", "a"));

        // Ascending order
        list.sort(Comparator.naturalOrder());
        System.out.println(list); // [A, B, C, a]

        // Descending order
        list.sort(Comparator.reverseOrder());
        System.out.println(list); // [a, C, B, A]
        
        // Ascending order without checking cases (uppercase and lowercase)
        list.sort(String.CASE_INSENSITIVE_ORDER);
        System.out.println(list); // [a, A, B, C]
        
        // Descending order without checking cases (uppercase and lowercase)
        list.sort(Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER));
        System.out.println(list);; // [C, B, a, A]
    }
}
```

###**`2. List.sort() with lambda`**
```java
import java.util.ArrayList;
import java.util.Arrays;

public class Sort {
    public static void main(String[] args) {

        // type1 : Integer
        ArrayList<String> list = new ArrayList<>(Arrays.asList(2, 4, 7, -1));

        list.sort((num1, num2) -> num1 - num2);

        list.sort((num1, num2) -> Integer.compare(num1, num2));

        list.sort(Integer::compare);

        // type2 : String
        ArrayList<String> list = new ArrayList<>(Arrays.asList("C", "A", "B", "a"));

        list.sort((s1, s2) -> s1.getAlphabet() - s2.getAlphabet());

        list.sort(comparing(English::getAlphabet)); // suppose there is a class 'English' which has a getter 'getAlphabet'
```
---

### `Important words`
- ascending  
- descending
