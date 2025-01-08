# Example Problem 1: Power of Two

## Problem Statement
Given an integer `n`, return `true` if it is a power of two. Otherwise, return `false`.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2^x`.

### Example Cases
1. Case 1:
>Input: n = 1
>
>Output: true
>
>Explanation: 2^0 = 1

2. Case 2:
>Input: n = 16
>
>Output: true
>
>Explanation: 24 = 16

3. Case 3:
>Input: n = 3
>
>Output: false
>
>Explanation: 3 cannot be a power of 2

### Constraints
`-2^31 <= n <= 2^31 - 1`

---
## Python Solution
```python
def isPowerOfTwo(n):
    # Base case: 1 is a power of two (2^0)
    if n == 1:
        return True
    # Base case: numbers less than 1 cannot be powers of two
    if n <= 0:
        return False
    # Recursive step: check if dividing n by 2 results in another power of two
    return n % 2 == 0 and isPowerOfTwo(n // 2)

# Example Usage
print(isPowerOfTwo(16))  # Output: True
print(isPowerOfTwo(4))   # Output: True
print(isPowerOfTwo(25))   # Output: False
```
---

### Explanation of the Solution
1. **Base Case 1**: If \( n == 1 \), return `True` because \( 1 \) is \( 2^0 \).
2. **Base Case 2**: If \( n \leq 0 \), return `False` because negative numbers and zero cannot be powers of two.
3. **Recursive Step**:
   - Check if \( n \) is divisible by 2 (\( n \% 2 == 0 \)).
   - If \( n \) is divisible, divide \( n \) by 2 and make a recursive call to \( \text{isPowerOfTwo}(n // 2) \).
   - Continue dividing until \( n \) becomes 1 (power of two) or is not divisible by 2.

### **Example Walkthrough**
**Input**: n = 16
1. **First call**: n = 16
   - `16 % 2 == 0`: True
   - Recursive call: isPowerOfTwo(16 // 2 = 8)
2. **Second call**: n = 8
   - `8 % 2 == 0`: True
   - Recursive call: isPowerOfTwo(8 // 2 = 4)
3. **Third call**: n = 4
   - `4 % 2 == 0`: True
   - Recursive call: isPowerOfTwo(4 // 2 = 2)
4. **Fourth call**: n = 2
   - `2 % 2 == 0`: True
   - Recursive call: isPowerOfTwo(2 // 2 = 1)
5. **Fifth call**: n = 1
   - Base case: `n == 1`: Return `True`.

Result: `n = 16` is a power of two, so the function returns `True`.
