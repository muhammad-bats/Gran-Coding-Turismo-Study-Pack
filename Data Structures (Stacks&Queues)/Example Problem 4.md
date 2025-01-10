# Example Problem 4: Implement Queue Using Stacks

## Problem Statement
Implement a first-in-first-out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue:
- `push(int x)`: Pushes element `x` to the back of the queue.
- `pop()`: Removes the element from the front of the queue and returns it.
- `peek()`: Returns the element at the front of the queue.
- `empty()`: Returns `true` if the queue is empty, `false` otherwise.

**Note:** You must use **only** standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.

### Example Cases

1. Case 1:
   > Input:
   > ```
   > ["MyQueue", "push", "push", "peek", "pop", "empty"]  
   > [[], [1], [2], [], [], []]
   > ```
   > Output:
   > ```
   > [null, null, null, 1, 1, false]
   > ``` 
   > Explanation:  
   > `MyQueue myQueue = new MyQueue()`;  
   > `myQueue.push(1); // queue is: [1]`  
   > `myQueue.push(2); // queue is: [1, 2]`  
   > `myQueue.peek(); // return 1`  
   > `myQueue.pop(); // return 1, queue is [2]`  
   > `myQueue.empty(); // return false`  

2. Case 2:
   > Input:
   > ```
   > ["MyQueue", "push", "push", "pop", "pop", "empty"]  
   > [[], [5], [10], [], [], []]
   > ```
   > Output:
   > ```  
   > [null, null, null, 5, 10, true]
   > ```
   > Explanation: 
   > `MyQueue myQueue = new MyQueue()`;  
   > `myQueue.push(5); // queue is: [5]`  
   > `myQueue.push(10); // queue is: [5, 10]`  
   > `myQueue.pop(); // return 5, queue is [10]`  
   > `myQueue.pop(); // return 10, queue is []`  
   > `myQueue.empty(); // return true`  

### Constraints:
`1 <= x <= 9`

At most `100` calls will be made to `push`, `pop`, `peek`, and `empty`.

All calls to `pop` and `peek` are valid.

---

## Python Solution
```python
class MyQueue:
    def __init__(self):
        self.stack_in = []  # Stack for pushing elements
        self.stack_out = []  # Stack for popping and peeking

    def push(self, x: int) -> None:
        self.stack_in.append(x)

    def pop(self) -> int:
        self._move()
        return self.stack_out.pop()

    def peek(self) -> int:
        self._move()
        return self.stack_out[-1]

    def empty(self) -> bool:
        return not self.stack_in and not self.stack_out

    def _move(self) -> None:
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
```

---

### Explanation of the Solution
The solution uses two stacks:
1. **`stack_in`**: For pushing elements into the queue.
2. **`stack_out`**: For popping and peeking elements from the queue.

**How it works:**
- When `push` is called, the element is added to `stack_in`.
- When `pop` or `peek` is called:
  - If `stack_out` is empty, all elements from `stack_in` are moved to `stack_out`. This reverses the order of elements, simulating a queue.
  - Then, the top of `stack_out` is popped or returned as needed.
- `empty` checks whether both stacks are empty.

This ensures that all operations adhere to the FIFO nature of a queue while using only stack operations.

### Example Walkthrough
**Input:**  
```
["MyQueue", "push", "push", "peek", "pop", "push", "peek", "empty"]  
[[], [7], [9], [], [], [11], [], []]
```
1. **`MyQueue myQueue = new MyQueue();`**
   - Output: `null`
   - Explanation: A new queue is initialized with empty stacks: `stack_in = []`, `stack_out = []`.

2. **`myQueue.push(7);`**
   - Output: `null`
   - Explanation: `7` is pushed into `stack_in`.  
     Current state: `stack_in = [7]`, `stack_out = []`.

3. **`myQueue.push(9);`**
   - Output: `null`
   - Explanation: `9` is pushed into `stack_in`.  
     Current state: `stack_in = [7, 9]`, `stack_out = []`.

4. **`myQueue.peek();`**
   - Output: `7`
   - Explanation: Since `stack_out` is empty, all elements from `stack_in` are moved to `stack_out` (reversed order).  
     `stack_out = [9, 7]`, `stack_in = []`.  
     The top of `stack_out` is `7`.

5. **`myQueue.pop();`**
   - Output: `7`
   - Explanation: The top of `stack_out` (`7`) is popped.  
     Current state: `stack_out = [9]`, `stack_in = []`.

6. **`myQueue.push(11);`**
   - Output: `null`
   - Explanation: `11` is pushed into `stack_in`.  
     Current state: `stack_in = [11]`, `stack_out = [9]`.

7. **`myQueue.peek();`**
   - Output: `9`
   - Explanation: The top of `stack_out` is `9`, so it is returned.

8. **`myQueue.empty();`**
   - Output: `false`
   - Explanation: Neither `stack_in` nor `stack_out` is empty.

**Output:**
```
[null, null, null, 7, 7, null, 9, False]
```
