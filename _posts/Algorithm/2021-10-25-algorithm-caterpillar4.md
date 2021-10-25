---
title:  "[Algorithm] Container With Most Water"
date: 2021-10-25 9:20PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Leetcode]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-25 9:20PM

---

# 'Container With Most Water' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/container-with-most-water/>

## 📌 Answer

### The point
- Used Caterpillar method
    - Start with the maximum width container and go to a shorter width container
        - Compare the left value and the right value
        - Square = width (j - i) * smaller height (height[i] vs [j])
        - i++ vs j--

[More detail about 'Caterpillar method'](https://uzzing.github.io/posts/caterpillar/)

[Result](https://leetcode.com/submissions/detail/576908075/)

```java
import java.lang.Math;

class Solution {
    public int maxArea(int[] height) {
    
        int i = 0;
        int j = height.length - 1;
        
        int max = 0;
        while (i < j) {
            if (height[i] < height[j])
                max = Math.max(max, (j - i) * height[i++]); // j-i : width
            else
                max = Math.max(max, (j - i) * height[j--]);
        }
        
        return max;
    }
}
/**
[Question]
return the container contains the most water
**/
```

The source : my head

---

I finally used caterpillar method I learned in Codility! <br>
Yeeees