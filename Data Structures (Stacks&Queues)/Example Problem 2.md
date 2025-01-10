# Example Problem 2: Limited Stack Implementation

## Problem Statement
Design a stack that supports basic stack operations like `push`, `pop`, `top`, and an additional operation to check if the stack is full.

Implement the `LimitedStack` class:

- `LimitedStack(int limit)` initializes the stack object with a size limit.
- `void push(int val)` pushes the element `val` onto the stack if it is not full. If the stack is full, the push operation should not do anything.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack. If the stack is empty, return `-1`.
- `bool isFull()` returns `true` if the stack is full, otherwise `false`.

You must implement a solution with O(1) time complexity for each function.

### Example Cases
1. Case 1:
> Input:
> ```  
> ["LimitedStack","push","push","push","push","top","pop","isFull"]  
> [[3],[1],[2],[3],[4],[],[],[]]  
> ```
> Output:
> ```  
> [null,null,null,null,null,3,null,true]  
> ```
> Explanation:  
> `LimitedStack stack = new LimitedStack(3);`  
> `stack.push(1);`  
> `stack.push(2);`  
> `stack.push(3);`  
> `stack.push(4); // Does not push because the stack is full.`  
> `stack.top(); // Returns 3 (top element)`  
> `stack.pop();`  
> `stack.isFull(); // Returns true since the stack has reached its limit.`

2. Case 2:
> Input:
> ```  
> ["LimitedStack","push","pop","top","isFull"]  
> [[2],[10],[],[],[]]  
> ```
> Output:
> ```  
> [null,null,null,-1,false]  
> ```
> Explanation:  
> `LimitedStack stack = new LimitedStack(2);`  
> `stack.push(10);`  
> `stack.pop();`  
> `stack.top(); // Returns -1 (stack is empty)`  
> `stack.isFull(); // Returns false since the stack is not full.`

### Constraints:
The stack limit will always be at least 1.

At most 10^4 calls will be made to `push`, `pop`, `top`, and `isFull`.

---

## Python Solution
```python
class LimitedStack:

    def __init__(self, limit: int):
        self.stack = []
        self.limit = limit
        
    def push(self, val: int) -> None:
        if len(self.stack) < self.limit:
            self.stack.append(val)
        
    def pop(self) -> None:
        if self.stack:
            self.stack.pop()
        
    def top(self) -> int:
        return self.stack[-1] if self.stack else -1

    def isFull(self) -> bool:
        return len(self.stack) == self.limit
```

---

### Explanation of the Solution
In this solution, the `LimitedStack` class uses a list called `stack` to store the elements. The stack has a maximum size, determined by the `limit` variable. The stack operations are designed as follows:
- **`push(val)`**: Adds `val` to the stack only if the current stack size is less than the limit.
- **`pop()`**: Removes the top element from the stack if it's not empty.
- **`top()`**: Returns the top element of the stack, or `-1` if the stack is empty.
- **`isFull()`**: Checks if the stack has reached its size limit by comparing the current size with the `limit`.

This implementation ensures that the operations are completed in constant time, O(1).

### Example Walkthrough
**Input:** 
```
["LimitedStack", "push", "push", "push", "push", "pop", "top", "isFull"]
[[3], [10], [20], [30], [40], [], []]
```

1. **`LimitedStack stack = new LimitedStack(3);`**
   - Creates a stack with a size limit of 3.
   - `null` output since nothing is returned.

2. **`stack.push(10);`**
   - `self.stack = [10]`
   - The stack has room, so `10` is added to it.
   - `null` output since nothing is returned.

3. **`stack.push(20);`**
   - `self.stack = [10, 20]`
   - The stack has room, so `20` is added to it.
   - `null` output since nothing is returned.

4. **`stack.push(30);`**
   - `self.stack = [10, 20, 30]`
   - The stack has room, so `30` is added to it.
   - `null` output since nothing is returned.

5. **`stack.push(40);`**
   - The stack is full, so no change occurs. 
   - `self.stack = [10, 20, 30]` (no new element added).
   - `null` output since nothing is returned.

6. **`stack.pop();`**
   - `self.stack = [10, 20]`
   - The top element, `30`, is removed.
   - `null` output since nothing is returned.

7. **`stack.top();`**
   - Returns `20` (the top element of the stack).

8. **`stack.isFull();`**
   - Returns `false` (the stack has space for more elements).

**Output:**
```
[null, null, null, null, null, null, 20, False]
```
