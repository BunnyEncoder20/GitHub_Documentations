- DSA problems can be made easier if we can start identifying the patterns which are happening over and over again:

# Sliding Window 

- When we need to process a DS like a list or string. And we need to process a smaller part of the list 
- This smaller part / segment of the DS is what we call a window. This window is slide over the entire DS till the it is fully processed.
- **Whenever we need to find a subset of elements within the list/string which satisfy a given condition, think of sliding window approach**
- The DS should be a linear DS like array, string, LinkedList
- Eg: Longest/shortest/maximum sum/minimum sum *sub-array* or *sub-string* problems 
	- Maximum Average SubArray I
	- Longest Substring without repeating characters
	- Minimum window substring

---

# Subset Problem

- **When we need to find all the combination of elements from a given set** (repetitions may or may not be allowed depending on the problem). We need to find all the possible arrangements of the given set of elements.
- Eg: Permutations / Combination problems

---

# Modified Binary Search

- **When ever there is a need to search for a element in a somewhat (nearly) sorted DS**
- Eg of such arrays include : 
	- searching in a nearly sorted array
	- searching in a rotated sorted array
	- searching in a list with unknown length
	- searching in a array with duplicates 
	- finding first or last occurance of a array
	- finding square root of a number 
	- finding peak element
- The core concept of Binary Search is to keep dividing the search space into half. 
- In modified Binary search, the core concept remains the same, but there are some modification added according to the problem.
- Python *bisect* library contains 2 functions : 
	- bisect.left() 
	- bisect.right()
- Implementing the above 2 functions will help in getting core understanding of Binary Search algorithm.
- To make modified Binary search codes, we must know simple binary search algorithm very well
- Eg:
	- Search in a rotated sorted array
	- Find minimum in a rotated sorted array
	- search in a 2D matrix II

---

# Top K elements

- **When we need to find the K top/bottom ranking elements from the larger DS**
- *Helps in finding the 'K' largest, smallest, most frequent* elements in a array.
- Eg: Find K largest numbers in an array
- Hence to solve it efficiently, we need to keep track of k of the most relevant elements.
- We store these elements in a Heap DS (cause it makes removing the smallest number very efficient and it avoids need to sort the array)
- Eg:
	- Kth largest element in an Array
	- Top k frequent elements 
	- Find K pairs with smallest sums

---

# Binary Tree Traversal

- **Binary Trees all about traversing it in a specific order**
- The 4 ways to traverse 
	- pre-order : root > left > right
	- in-order : left > root > right
	- post-order : left > right > root
	- level-order : level by level
- Traversals are easier if we implement them using **recursion**
- Whenever given a tree traversal problem, think about which DS fits the best. Eg:
	- To retrieve the values of a binary tree in sorted order, use *inorder traversal*
	- to create a copy of the tree (or tree serialisations problems) use *preorder traversal*
	- When we want to process child node before the parent node (when deleting a node) use *postorder traversal*
	- When we need to explore all nodes at the current level before moving onto the next, use *Level order traversal*
- Eg problems:
	- Binary Tree paths
	- Kth smallest element in a BST
	- binary tree maximum path sum
	- Binary tree level order traversal II

---

# Topological Sort

- **Used when we need to arrange elements in such a way that they are some dependency on each other. Mostly useful for directed Acyclic Graphs**
- *think of this approach when you have a pre-requisite chain* : we need to do this but it has certain pre-requisites which need to be done before that.
- Directed Acyclic graph =
	- one way direction 
	- no cycles / loops
- Eg : Course Schedule Problem

---

# BFS

- **Traversal technique which goes level by, but need to explore all the nodes at the same level, before going down to the next level, in a tree or graph**
- We do this using a Queue DS. 
- Useful for problems like :
	- finding shortest path between 2 nodes 
	- printing all nodes of a tree level by level
	- finding all connected components in a graph
	- finding shortest transformation sequence between one word to another 
- Eg problems:
	- Binary tree level order traversal
	- Rotting oranges 
	- word ladder

---

# 2 Pointer 

- **Used when we need to iterate through a sorted array and we need to 2 pointers to move according to each other**
- This is a very important pattern as it helps in reducing the Time complexity of many problems from O(n^2) to O(n).
- Eg: Two Sum II , 3Sum, Container with Most Water

---

# Prefix Sum

- **Common when we need to query SUM OF ELEMENTS IN A SUBARRAY**
- Example : 
	- we need to find sum of elements between index i and j. 
	- though it can be solved using a single loop from i to j, if there are multiple such queries, we would need to optimize.
	- Can do this by creating prefix sum array, which would contain the sum of all the elements till that index. So then the sum of elements between i and j would be sum[j]-sum[i].
	- If we do not want to use extra space we can directly modify the original array to save space.
- Eg;
	- Range Sum Query - Immutable
	- Contiguous Array
	- SubArray Sum Equals K

---

# Fast and Slow Pointers

- **Used in Linked Lists and Arrays where we want to find cycles within these DS**
- We move the 2 pointers are different speeds and when they meet, it proves a cycle is present within the linkedlist.
- It can also find the mid point of an LinkedList within one pass.
- Eg;
	- LinkedList Cycle
	- Happy Number
	- Find duplicate Number

---

# Linked List in-place Reversal

- Many problems require us to reverse a linkedlist. The brute force for the same requires extra space equal to the linked list itself and multiple passes of the DS
- To do it in a single pass and without using extra space we use **3 pointers - prev, curr, next** and use these to modify the pointers of the nodes.
- Eg:
	- Reverse LinkedList 
	- Reverse LinkedList II
	- Swap nodes in Pairs

---

# Monotonic Stack

- **This pattern uses a stack DS to find the next greatest and next smallest element in a array**
- Eg:
	- Next Greatest element I
	- Daily Temperatures
	- Largest rectangle in Histogram

---

# Overlapping Intervals 

- **Pattern seen when problems have intervals or ranges that may overlap.**
- Few problem types which may apply these patterns : 
	- **Merging Intervals** - given a collection of intervals, merge the overlapping intervals into one
	- **Interval Intersection** - find the intersection between 2 intervals 
	- **Insert Intervals** - add a interval into a collection of non overlapping intervals 
	- **Find minimum number of meeting rooms** - without overlapping meeting times

---

# DFS 

- **Used to explore all paths or branches in graphs or trees**
- Eg:
	- finding a path between 2 nodes 
	- checking if a graph contains a cycle
	- finding topological order in a acyclic graph
	- counting the number of connected components in a graph 
- Eg problems:
	- Clone graph
	- Path sum II
	- Course schedule II

---

# Matrix Traversal 

- **Mostly seen in  graph problems**
- Most of the graph algorithms like BFS,DFS work in matrix as well. Eg:
	- finding shortest path in a grid
- Eg problems :
	- flood fill
	- number of islands
	- surrounded regions

---

# BackTracking

- **Exploring all potential solution path and backtracking the paths that do not lead to a valid solution**
- Eg: 
	- generate all permutations / combinations of a given set of elements 
	- Solve puzzles like sudoku or n-queens
	- find all paths from a start to end point in a maze
	- generate all valid parenthesis of a given length 
- Eg problems:
	- Permutations 
	- subsets
	- n-queens

---

# Dynamic Programming

- **Used for solving optimisation problems by breaking them down into smaller sub-problems ans storing their solutions to avoid repetitive work**
- Particularly useful for maximising/minimising a certain value or counting number of ways problems
- Common DP patterns:
	- Fibonacci Numbers
	- 0/1 Knapsack
	- Longest Common Subsequence
	- Longest increasing subsequence 
	- subset sum
	- Matrix chain multiplication
- Eg problems: 
	- Climbing stairs 
	- Coin change
	- Longest Common Subsequence
	- Partition Equal subset sum
	- Burst Ballons