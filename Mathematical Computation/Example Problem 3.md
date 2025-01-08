# Example Problem 3: Add Digits

## Problem Statement
Given an integer `num`, repeatedly add all its digits until the result has only one digit, and return it.

### Example Cases
1. Case 1:
>Input: num = 38
>
>Output: 2
>
>Explanation: The process is
>
>38 --> 3 + 8 --> 11
>
>11 --> 1 + 1 --> 2 
>
>Since 2 has only one digit, it is returned.

2. Case 2:
>Input: num = 54
>
>Output: 9
>
>Explanation:
>
>54 --> 5 + 4 --> 9

### Constraints
`0 < = num <= 2^31 - 1`

---
## Python Solution
```python
def add_digits(num):
    # Using the digital root formula
    if num == 0:
        return 0
    return 1 + (num - 1) % 9 if num > 0 else num
```
---

### Explanation of the Solution
The solution is based on the concept of the **digital root**, which can be computed without repeatedly summing the digits. Here's how it works:
1. **Digital Root Concept**:
   - A number's digital root is the result of repeatedly summing its digits until a single digit is obtained.
   - Mathematically, the digital root can be computed as:
     - If `num == 0`: The result is `0`.
     - Otherwise: `digital_root = 1 + (num - 1) % 9`.
2. **Why This Formula Works**:
   - The digital root is equivalent to the remainder when dividing a number by 9, except when the number is `0` (special case).
   - This avoids the need for explicit summation and significantly improves efficiency.
3. **Edge Case**:
   - If `num == 0`, return `0`.

### Example Walkthrough
**Input:** `num = 2025`
1. Apply the formula:  
   - Compute `(2025 - 1) % 9`:  
     - `2025 - 1 = 2024`
     - `2024 % 9 = 8`
   - Add `1` to the result: `1 + 8 = 9`

**Output:** `9`
