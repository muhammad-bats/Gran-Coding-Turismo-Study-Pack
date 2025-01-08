# Example Problem 1: Reverse Integer

## Problem Statement
Given a signed 32-bit integer `x`, return `x` with its *digits reversed*. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

### Example Cases
1. Case 1:
>Input: x = 123
>
>Output: 321

2. Case 2:
>Input: x = -123
>
>Output: -321

3. Case 3:
>Input: x = 120
>
>Output: 210

### Constraints
`-2^31 < = x < = 2^31 - 1`

---
## Python Solution
```python
def reverse(x):
    # Define the 32-bit signed integer range
    INT_MIN, INT_MAX = -2**31, 2**31 - 1
    
    # Extract the sign of x
    sign = -1 if x < 0 else 1
    
    # Reverse the digits of the absolute value of x
    reversed_num = int(str(abs(x))[::-1])
    
    # Check if the reversed number exceeds the 32-bit range
    if reversed_num < INT_MIN or reversed_num > INT_MAX:
        return 0
    
    # Return the reversed number with the correct sign
    return sign * reversed_num
```
---

### Explanation of the Solution
1. **Handling the 32-bit Range**:
   - Define the 32-bit signed integer range as `[-2^31, 2^31 - 1]` (from -2147483648 to 2147483647). Any number outside this range should return `0`.
2. **Extracting the Sign**:
   - If `x` is negative, the `sign` variable is set to `-1`. Otherwise, it is `1`.
3. **Reversing the Digits**:
   - Use `abs(x)` to get the absolute value of `x`.
   - Convert the number to a string, reverse the string using slicing (`[::-1]`), and convert it back to an integer.
4. **Checking for Overflow**:
   - If the reversed number exceeds the 32-bit range, return `0`.
5. **Returning the Result**:
   - Multiply the reversed number by its original sign (`sign`) to restore its positive or negative nature.

### Example Walkthrough
**Input**: `x = -123`  
**Execution**:
1. `sign = -1` (since `x` is negative).
2. `abs(x) = 123` → Reverse digits: `"123"[::-1]` → `321`.
3. Check if `321` is within the range `[-2^31, 2^31 - 1]` → Yes.
4. Return `-1 * 321 = -321`.

**Output**: `-321`
