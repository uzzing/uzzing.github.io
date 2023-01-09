---
title:  "[Data Sturcture] LinkedList (vs ArrayList)"
date: 2023-1-9 5:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-9 5:00PM
---

# LinkedList Method List

- Often using [*First] methods
    - addFirst
    - peekFirst
    - pollFirst
    - removeFirst

![Screen Shot 2023-01-09 at 5 29 11 PM](https://user-images.githubusercontent.com/83699657/211266957-e0143316-2190-4084-9ba9-14e9a5498b5c.png)

![Screen Shot 2023-01-09 at 5 31 29 PM](https://user-images.githubusercontent.com/83699657/211267073-8d97cb63-76a1-48d3-ba6c-68b98e4e62c0.png)

```java

// if you want to make the reverse order list, use addFirst()

LinkedList<Integer> list = new LinkedList<>();
list.addFirst(1);
list.addFirst(2);
list.addFirst(3);

// list -> [3, 2, 1]

```

# ArrayList VS LinkedList

- Manipulation with LinkedList is **faster** than ArrayList

![Screen Shot 2023-01-09 at 5 35 15 PM](https://user-images.githubusercontent.com/83699657/211267633-6a69ba80-9094-4ba4-a8b5-c7467776bd92.png)

- Reference 
: <https://www.javatpoint.com/difference-between-arraylist-and-linkedlist>