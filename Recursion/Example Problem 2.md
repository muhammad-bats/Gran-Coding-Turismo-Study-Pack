# Example Problem 2: Fibonacci Sequence

## Problem Statement
The Fibonacci numbers, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

>F(0) = 0, F(1) = 1
>
>F(n) = F(n - 1) + F(n - 2), for n > 1.

### Task
Given `n`, calculate `F(n)`.

### Example Cases
1. Case 1:
>Input: n = 2
>
>Output: 1
>
>Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.

2. Case 2:
>Input: n = 3
>
>Output: 2
>
>Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.

3. Case 3:
>Input: n = 4
>
>Output: 3
>
>Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.

### Constraints
`0 < = n < = 30`

---
## Python Solution
```python
def fib(n):
    # Base cases
    if n == 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    return fib(n - 1) + fib(n - 2)

# Example Usage
print(fib(2))  # Output: 1
print(fib(5))  # Output: 5
print(fib(7))  # Output: 13
```
---

### **Explanation of the Solution**

1. **Base Cases**:
   - If `n = 0`, the Fibonacci value is 0 ( `F(0) = 0` ).
   - If `n = 1`, the Fibonacci value is 1 ( `F(1) = 1` ).
   - These base cases terminate the recursion.

2. **Recursive Case**:
   - For `n > 1`, calculate the Fibonacci value as:
     
     `F(n) = F(n - 1) + F(n - 2)`
     
   - This breaks the problem into smaller subproblems, eventually reaching the base cases.

3. **Recursive Calls**:
   - The function recursively computes `F(n - 1)` and `F(n - 2)`, summing their results to compute `F(n)`.

### **Example Walkthrough**
**Input:** `n = 5`
1. **First call**: `fib(5)`
   - `n > 1`: Calculate `fib(4) + fib(3)`
2. **Second call**: `fib(4)`
   - `n > 1`: Calculate `fib(3) + fib(2)`
3. **Third call**: `fib(3)`
   - `n > 1`: Calculate `fib(2) + fib(1)`
4. **Base calls**: Compute `fib(2) = 1`, `fib(1) = 1`, and `fib(0) = 0`.

Here’s the complete calculation:
   - `fib(0) = 0`
   - `fib(1) = 1`
   - `fib(2) = fib(1) + fib(0) = 1 + 0 = 1`
   - `fib(3) = fib(2) + fib(1) = 1 + 1 = 2`
   - `fib(4) = fib(3) + fib(2) = 2 + 1 = 3`
   - `fib(5) = fib(4) + fib(3) = 3 + 2 = 5`

Result: `F(5) = 5`.
