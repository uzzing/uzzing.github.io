---
title:  "[Development] Exception In Java"
date: 2022-10-12 5:00PM
excerpt: "Dev"

author: Yuha
categories: [Development]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-10-12 5:00PM
---

# Exception in Java

<img width="1146" alt="Screen Shot 2022-10-12 at 5 22 13 PM" src="https://user-images.githubusercontent.com/83699657/195290222-038635ef-6fb7-411e-bb88-eb5523b9c017.png">

---

# Checked Exception vs Unchecked Exception

||**Checked Exception**|**Unchecked Exception**|
|:---:|:---:|:---:|
|When checked|**checked** at compile time.|**not checked** at compile time, it **occurs at runtime**.|
|Handling exception|A checked **must be handled** either by re-throwing or with a try-catch block|whereas an unchecked **isn't required** to be handled.|

<img width="804" alt="Screen Shot 2022-10-12 at 5 39 11 PM" src="https://user-images.githubusercontent.com/83699657/195294155-f4232644-ce1c-41e1-b930-3bb8d651f5ea.png">

---

# Checked Exception
- These are the exceptions that are checked at compile time.
- If some code within a method throws a checked exception, then the method **must either handle the exception** or it must specify the exception using the throws keyword.

## A fully checked exception
- A fully checked exception is a checked exception where **all its child classes are also checked**, like IOException, InterruptedException.

## A partially checked exception
- A partially checked exception is a checked exception where **some of its child classes are unchecked**, like Exception.

---

# Unchecked Exception
- These are the exceptions that are not checked at compile time.
- It is **not forced** by the compiler to either **handle or specify the exception.** It is up to the programmers to be civilized, and specify or catch the exceptions.


---

[Reference]
- <https://facingissuesonit.com/java-exception-handling/>

- <https://www.geeksforgeeks.org/checked-vs-unchecked-exceptions-in-java/>

- <https://www.theserverside.com/answer/What-are-checked-vs-unchecked-exceptions-in-Java>