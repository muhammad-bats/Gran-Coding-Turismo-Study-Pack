# Example Problem 1: Add Binary

## Problem Statement
Given two binary strings `a` and `b`, return *their sum as a binary string.*

### Example Cases
1. Case 1:
>Input: a = "11", b = "1"
>
>Output: "100"

2. Case 2:
>Input: a = "1010", b = "1011"
>
>Output: "10101"

### Constraints
`1 < = a.length, b.length < = 10^4`

`a` and `b` consist only of `'0'` or `'1'` characters.

Each string does not contain leading zeros except for the zero itself.

---
## Python Solution
```python
def addBinary(a, b):
    # Initialize pointers for both strings starting from the last digit
    i, j = len(a) - 1, len(b) - 1
    carry = 0  # Carry from addition
    result = []

    while i >= 0 or j >= 0 or carry:
        # Extract bits from a and b
        bit_a = int(a[i]) if i >= 0 else 0
        bit_b = int(b[j]) if j >= 0 else 0

        # Calculate the sum of bits and carry
        total = bit_a + bit_b + carry
        result.append(str(total % 2))  # Add the result bit
        carry = total // 2  # Update the carry

        # Move pointers
        i -= 1
        j -= 1

    # Reverse the result list to get the final binary sum
    return ''.join(result[::-1])
```

---

### Explanation of the Solution

1. **Pointers for Strings**:
   - Two pointers, `i` and `j`, start from the last indices of `a` and `b`, respectively.

2. **Bit Addition**:
   - At each step, the bits of `a` and `b` at indices `i` and `j` are extracted (or `0` if out of bounds).
   - Add these bits along with the carry to compute the current digit and update the carry.

3. **Result Construction**:
   - Append the current digit (as a string) to a result list.
   - At the end of the loop, reverse the list and join it into a single binary string.

4. **Edge Cases**:
   - If one string is shorter, treat missing bits as `0`.
   - Include a final carry if present.


### Example Walkthrough

**Input:**

```python
a = "1101"
b = "101"
```
1. **Initial State**:
   - `a = "1101"`, `b = "101"`, `carry = 0`, `result = []`

2. **Step 1 (i = 3, j = 2)**:
   - `bit_a = 1`, `bit_b = 1`
   - `total = 1 + 1 + 0 = 2`
   - `result = ['0']`, `carry = 1`

3. **Step 2 (i = 2, j = 1)**:
   - `bit_a = 0`, `bit_b = 0`
   - `total = 0 + 0 + 1 = 1`
   - `result = ['0', '1']`, `carry = 0`

4. **Step 3 (i = 1, j = 0)**:
   - `bit_a = 1`, `bit_b = 1`
   - `total = 1 + 1 + 0 = 2`
   - `result = ['0', '1', '0']`, `carry = 1`

5. **Step 4 (i = 0, j = -1)**:
   - `bit_a = 1`, `bit_b = 0`
   - `total = 1 + 0 + 1 = 2`
   - `result = ['0', '1', '0', '0']`, `carry = 1`

6. **Step 5 (i = -1, j = -1)**:
   - `bit_a = 0`, `bit_b = 0`
   - `total = 0 + 0 + 1 = 1`
   - `result = ['0', '1', '0', '0', '1']`, `carry = 0`

7. **Final Result**:
   - Reverse `result`: `['1', '0', '0', '1', '0']`
   - Output: `"10010"`

**Output:** `"10010"`
