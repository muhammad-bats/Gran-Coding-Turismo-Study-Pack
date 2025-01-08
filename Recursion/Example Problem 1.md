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
    # A number is a power of two if it is greater than 0
    # and its binary representation contains exactly one '1'.
    return n > 0 and (n & (n - 1)) == 0

# Example Usage
n1 = 4
n2 = 16
n3 = 30
print(isPowerOfTwo(n1))  # Output: True
print(isPowerOfTwo(n2))  # Output: True
print(isPowerOfTwo(n3))  # Output: False
```

---

## Explanation of the Solution

1. **Key Insight:**
   - A number \( n \) is a power of two if and only if it is greater than 0 and its binary representation contains exactly one '1'.
   - For example:
     - \( 1 \) (binary: `0001`) is a power of two.
     - \( 16 \) (binary: `10000`) is a power of two.
     - \( 3 \) (binary: `0011`) is **not** a power of two.

2. **Using the Bitwise Trick:**
   - For any power of two \( n \), the expression \( n \& (n - 1) \) will always be \( 0 \).
     - Example: \( n = 4 \) (binary: `0100`)
       - \( n - 1 = 3 \) (binary: `0011`)
       - \( n \& (n - 1) = 0100 \& 0011 = 0000 \)
   - This works because subtracting 1 from \( n \) flips the least significant '1' in \( n \) and all the bits to the right of it.

3. **Algorithm Steps:**
   - Check if \( n > 0 \). Power of two numbers must be positive.
   - Use the bitwise expression \( n \& (n - 1) == 0 \) to check if \( n \) is a power of two.
   - Return the result.

### Example Walkthroughs
**Input**: \( n = 16 \)

1. Check if \( n > 0 \): \( 16 > 0 \) (True).
2. Calculate \( n \& (n - 1) \):
   - Binary of \( n = 16 \): `10000`
   - Binary of \( n - 1 = 15 \): `01111`
   - \( 10000 \& 01111 = 00000 \)
3. Result: \( n \& (n - 1) == 0 \) (True).

**Output**: **True** (16 is a power of two).
