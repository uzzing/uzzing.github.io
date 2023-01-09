---
title:  "[Data Sturcture] Tree Traversal (preorder, inorder, postorder)"
date: 2023-1-9 2:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-9 5:30PM
---

# Tree Traversal 
![Screen Shot 2023-01-09 at 2 32 07 PM](https://user-images.githubusercontent.com/83699657/211246575-86367747-0d0d-4888-b223-ed4cde982d11.png)

- preorder traversal
    - A -> B -> D -> H -> I -> E -> C -> F -> G
- inorder traversal
    - H -> D -> I -> B -> E -> A -> F -> C -> G 
- postorder traversal
    - H -> I -> D -> E -> B -> F -> G -> C -> A


- Reference
: <<https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=4717010&logNo=60209908735>


# Example : preorder traversal 

## Problem
<https://leetcode.com/problems/binary-tree-preorder-traversal/>

## Result
```
Input: root = [1,null,2,3]
Output: [1,2,3]
```

## Answer 

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if (root == null) return result;

        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            if (node.right != null) stack.push(node.right);
            if (node.left != null) stack.push(node.left);
        }
        
        return result;
    }
}
```

- Reference
: <https://leetcode.com/problems/binary-tree-preorder-traversal/solutions/45417/preorder-traversal-java-solution-both-iteration-and-recursion/?orderBy=most_votes&languageTags=java>


# Example : postorder traversal 

## Problem
<https://leetcode.com/problems/binary-tree-postorder-traversal/>

## Result
```
Input: root = [1,null,2,3]
Output: [3,2,1]
```

## Answer 
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> result = new LinkedList<>();
        if (root == null) return result;

        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);

        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.addFirst(node.val); // difference
            if (node.left != null) stack.push(node.left); // difference
            if (node.right != null) stack.push(node.right); // difference
        }
        return result;
    }
}
```

- Reference :
<https://leetcode.com/problems/binary-tree-postorder-traversal/solutions/45556/java-simple-and-clean/?orderBy=most_votes&languageTags=java>