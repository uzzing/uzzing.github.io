---
title:  "[Algorithm] DFS vs BFS"
date: 2021-10-21 2:20PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-21 9:11PM
---
# DFS vs BFS
---
## 📌 Let's compare

![bfs-dfs](https://user-images.githubusercontent.com/83699657/138210966-cf002fa1-ee52-45e3-a775-a2fa5a13e859.png)

||BFS|DFS|
|:---:|:---|:---|
|Full form|Breadth-First Search|Depth-First Search|
|Data structure often used | BFS uses **Queue** data structure for finding the shortest path. (FIFO)| DFS uses **Stack** data structure to remember the nodes already is visited (LIFO) |
|Features| BFS is better when target is **closer** to Source.<br> -> There is no need of backtracking. | DFS is better when target is **far** from source<br> -> There is a need of backtracking.<br> -> There is a possibility that it visit all nodes.|
| Advantages | A BFS will **find the shortest path** between the starting point and any other reachable node| - A DFS on a binary tree generally **requires less memory** than BFS. <br> - DFS can be **easily implemented with recursion**. |
| Disadvantages | A BFS on a binary tree generally requires more memory than a DFS.| A DFS doesn't necessarily find the shortest path to a node, while DFS does. |
|Situation| - A problem requiring the shortest path | - A problem that you must store the features of each path |

---
## 📌 Implementation
### **1. BFS**
#### - Used queue
```java
class Graph { 

    private int V; 
    private LinkedList<Integer> adj[]; 
    
    Graph(int v) { 
        V = v; 
        adj = new LinkedList[v]; 
        for (int i=0; i<v; ++i) adj[i] = new LinkedList(); 
    } 
    
    void addEdge(int v, int w) { 
        adj[v].add(w); 
    } 
    
    /* BFS */ 
    void BFS(int s) { 
        
        boolean visited[] = new boolean[V]; 

        LinkedList<Integer> queue = new LinkedList<Integer>(); 
        
        // Big difference with DFS
        // use queue features (FIFO)
        visited[s] = true; 
        queue.add(s); 

        while (queue.size() != 0) { // = (!queue.isEmpty()) 
            // get the first node and delete it from queue
            s = queue.poll(); 
            System.out.print(s + " "); 
            
            // get other nodes near the node which visit
            Iterator<Integer> i = adj[s].listIterator(); 
            
            while (i.hasNext()) { 
                int n = i.next(); 
                
                // if it is not a node which is already visited, check visiting and send to the last
                if (!visited[n]) { 
                    visited[n] = true;
                    queue.add(n); 
                } 
            }

            /** This expression is also okay

            Queue<Integer> q = new LinkedList<Integer>();
	    q.offer(v);
	    visited[v] = true;

            for (int i = 1; i < n+ 1 ; i++) {
                if (map[vv][i] == 1 && !visited[i]) {
                    q.offer(i);			// visit map[vv][i~n]
                    visited[i] = true;
                }
	    }
            **/
        }
    }
}
```
### **2. DFS**
#### - Used stack
```java
static int map[][];
static boolean[] visited;	
static String answer = "";

public static void dfs_stack(int v) {

	Stack<Integer> stack = new Stack<Integer>();
	stack.push(v);
	
	while (!stack.isEmpty()) {
		int vv = stack.pop();
		visited[vv] = true;	
		answer += vv + " ";
		
		for (int i = 1; i < n + 1; i++) {
			if (map[vv][i] == 1 && !visited[i]) {
				stack.push(i);
				break; // Big difference with BFS
			}
		}
	}
}
```
#### - Used recursion
```java
class Graph { 

    private int V;
    private LinkedList<Integer> adj[];
    
    Graph(int v) { 
        V = v; 
        adj = new LinkedList[v]; 
        
        // initialization
        for (int i=0; i < v; ++i) adj[i] = new LinkedList(); 
    } 
    
    void addEdge(int v, int w) { 
        adj[v].add(w); 
    } 
    
    /* DFS */ 
    void DFS(int v) { 
        boolean visited[] = new boolean[V]; 
        
        // Big difference with BFS
        // recursion with v as the starting node
        DFSUtil(v, visited); 
    } 
    
    // recursion
    void DFSUtil(int v, boolean visited[]) { 
        // store the node already is visited 
        visited[v] = true; 
        System.out.print(v + " "); 
        
        // get other nodes near the node which visit
        Iterator<Integer> it = adj[v].listIterator();
        while (it.hasNext()) { 
            int n = it.next(); 
            
            // if it is not a node which is already visited, revoke DFSUtil 
            if (!visited[n]) DFSUtil(n, visited); 
        }
    }
}

```
** the source 
: <https://devuna.tistory.com/32>
<https://velog.io/@ming/DFS-vs-BFS-탐색>
