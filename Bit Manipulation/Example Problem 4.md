# Example Problem 4: Sum of Two Integers

## Problem Statement
Given two integers `a` and `b`, return the sum of the two integers without using the operators `+` and `-`.

### Example Cases
1. Case 1:
>Input: a = 1, b = 2
>
>Output: 3

2. Case 2:
>Input: a = 2, b = 3
>
>Output: 5

### Constraints
`-1000 < = a, b < = 1000`

---
## Python Solution

```python
def getSum(a: int, b: int) -> int:
    # Define mask for 32 bits to handle overflow
    MASK = 0xFFFFFFFF
    MAX_INT = 0x7FFFFFFF

    while b != 0:
        # Calculate carry
        carry = (a & b) & MASK
        # Sum without carry
        a = (a ^ b) & MASK
        # Shift carry to the left
        b = (carry << 1) & MASK

    # Handle negative numbers
    return a if a <= MAX_INT else ~(a ^ MASK)
```

---

### Explanation of the Solution

1. **Key Idea**:
   - The task is to sum two integers without using `+` or `-`. Instead, we use bitwise operations: `AND`, `XOR`, and `LEFT SHIFT`.

2. **Breaking Down the Logic**:
   - **XOR (`a ^ b`)**: Adds the numbers without carrying over the 1s. This gives the preliminary sum.
   - **AND (`a & b`)**: Identifies the carry, i.e., where both `a` and `b` have 1s in the same bit position.
   - **LEFT SHIFT (`<< 1`)**: Moves the carry to the left by one bit to add it to the next higher bit in the next iteration.

3. **Handling 32-bit Integers**:
   - Use a **mask** (`0xFFFFFFFF`) to simulate 32-bit overflow. This ensures we only consider the lower 32 bits during calculations.
   - Handle **negative numbers**:
     - For Python, which doesn't have fixed-width integers, we need to explicitly interpret the result as a signed 32-bit integer. If the result exceeds the maximum positive integer (`0x7FFFFFFF`), we convert it to its negative equivalent using `~`.

4. **Termination**:
   - The loop continues until there is no carry left (i.e., `b == 0`).

### Example Walkthrough

**Input**:  
```
a = 4, b = 5
```
1. **Initial Values**:  
   - `a = 4 (0000 0100 in binary)`  
   - `b = 5 (0000 0101 in binary)`  

2. **First Iteration**:  
   - Carry: `(a & b) = 4 (0000 0100)`  
   - Preliminary Sum: `(a ^ b) = 1 (0000 0001)`  
   - Shifted Carry: `carry << 1 = 8 (0000 1000)`  
   - Update: `a = 1, b = 8`

3. **Second Iteration**:  
   - Carry: `(a & b) = 0 (0000 0000)`  
   - Preliminary Sum: `(a ^ b) = 9 (0000 1001)`  
   - Shifted Carry: `carry << 1 = 0 (no carry)`  
   - Update: `a = 9, b = 0`

4. **Result**:  
   - `a = 9`  
   - `b = 0` (no carry left, loop ends)

**Output**: `9`
