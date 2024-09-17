- This is a **very important** topic so understand it in depth. 
- This is because all the advance topics (Trees, Graphs, DP, etc) use recursion extensively.

## Basic Recursion

- It involves the following : 
```python
def func():
	if (base condition) : return 

	# function logic here

	func()    # recursively call the func
```

- Base / stopping condition is which will stop the recursive calls. 
- Recursion makes the computer store all the functions calls made. All these are stored in memory in something called a recursion stack. 
- The space taken by this stack is called *recursive stack space*
- **Stack Overflow** occurs when there is a infinite recursion calls (cause machines only have limited memory) or the base condition is never met.

## Head & Tail Recursion

- The above sample is a example of *head recursion* where *first* the function does it's job and *then* recursively calls itself.
- Most of the time we will be writing head recursion only.
```python
class Solution:
    maxRecursion = 5
    currentRecursion = 0
    
    def printNameRecursively(self, name):
	    # base condition
        if self.currentRecursion == self.maxRecursion:
            return
            
        # Function work done
        self.currentRecursion += 1
        print(name)
        
        # recursive call
        self.printNameRecursively(name)
```

- *Tail recursion* is the opposite, with first the recursive call is made and then the work is done.
- Modifying the above example itself:
```python
class Solution:
    maxRecursion = 5
    currentRecursion = 0
    
    def printNameRecursively(self, name):
	    # base condition
        if self.currentRecursion == self.maxRecursion:
            return
            
		# recursive call
        self.currentRecursion += 1
        self.printNameRecursively(name)
        
	    # Function work done
	    print(name)
```


## Recursion Tree

- It is how we visualise how the recursion is occurring
- We draw what the calls would occur and how the program flow will return (come back) from the calls.
- This *coming back* is also sometimes called **Back tracking**
![[Pasted image 20240917094200.png]]


## Time and Space Complexity 

- Assuming that there is no loop inside the function itself, then each function call can have `TC = O(1)`. If the function is recursively called for `n` number of times, then `TC = O(1) * O(n)` making it **TC = O(n)**
- Again if no extra space is being used in the function logic, then `SC = O(1) * O(n)` making the **SC = O(n)** (but this is purely the space taken by the machine's *recursive stack space* not the code itself).
- If there was more space being used by the code, example O(s) then the over all `SC = O(n) + n*O(s)`

## Recursion with params

- When we want to do a certain thing `n` number of times and want to return a result, we usually do it in the following pattern:
- Eg : Sum of N natural numbers
```python
class Solution:
    def recursiveSum(self, n):
        if n == 0: return 0
        else: return n + self.recursiveSum(n-1)
```
