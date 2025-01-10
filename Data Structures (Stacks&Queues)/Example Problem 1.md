# Example Problem 1: Min Stack Implementation

## Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

### Example Cases
1. Case 1:
>Input:  
> ```
> ["MinStack","push","push","push","getMin","pop","top","getMin"]  
> [[],[-2],[0],[-3],[],[],[],[]]
> ```  
>Output:  
> ```
> [null,null,null,null,-3,null,0,-2]  
> ```
>Explanation:  
> `MinStack minStack = new MinStack();`  
> `minStack.push(-2);`  
> `minStack.push(0);`  
> `minStack.push(-3);`  
> `minStack.getMin(); // return -3`  
> `minStack.pop();`  
> `minStack.top();    // return 0`  
> `minStack.getMin(); // return -2`

### Constraints:
`-2^31 < = val < = 2^31 - 1`

Methods `pop`, `top`, and `getMin` will always be called on non-empty stacks.

At most 3 * 10^4 calls will be made to `push`, `pop`, `top`, and `getMin`.

---

## Python Solution
```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = []
        
    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)
        
    def pop(self) -> None:
        val = self.stack.pop()
        if val == self.min_stack[-1]:
            self.min_stack.pop()
        
    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```

---

### Explanation of the Solution
To implement a stack that retrieves the minimum element in constant time, we use two stacks:
- `self.stack` holds the actual values of the stack.
- `self.min_stack` keeps track of the minimum values.

When pushing a value, we append it to both stacks. If the value is smaller than or equal to the current minimum (i.e., the top of `min_stack`), it is also appended to `min_stack`.

When popping a value, if the value matches the current minimum (the top of `min_stack`), we pop from `min_stack` as well.

The `getMin()` function simply returns the top of `min_stack`, which always holds the current minimum value.

### Example Walkthrough
Let’s walk through an example with the input `["MinStack", "push", "push", "push", "getMin", "pop", "top", "getMin"]` and the values `[[], [-2], [0], [-3], [], [], [], []]`.

1. **`MinStack minStack = new MinStack();`**
   - Creates an empty stack object.
   - `null` output since nothing is returned.

2. **`minStack.push(-2);`**
   - `self.stack = [-2]`
   - `self.min_stack = [-2]` (since -2 is the minimum value)
   - `null` output since nothing is returned.

3. **`minStack.push(0);`**
   - `self.stack = [-2, 0]`
   - `self.min_stack = [-2]` (since 0 is not less than -2)
   - `null` output since nothing is returned.

4. **`minStack.push(-3);`**
   - `self.stack = [-2, 0, -3]`
   - `self.min_stack = [-2, -3]` (since -3 is smaller than -2)
   - `null` output since nothing is returned.

5. **`minStack.getMin();`**
   - Returns `-3` (the minimum value in `self.min_stack`).
   - `3` output since it is returned.

6. **`minStack.pop();`**
   - Removes the top value, which is -3.
   - `self.stack = [-2, 0]`
   - `self.min_stack = [-2]` (since -3 was the minimum and was popped)
   - `null` output since nothing is returned.

7. **`minStack.top();`**
   - Returns `0` (the new top of `self.stack`).
   - `0` output since it is returned.

8. **`minStack.getMin();`**
   - Returns `-2` (the current minimum value from `self.min_stack`).
   - `-2` output since it is returned.
**Output**:
```
[null,null,null,null,-3,null,0,-2]  
```
