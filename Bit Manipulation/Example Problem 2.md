# Example Problem 2: Single Number

## Problem Statement
Given a **non-empty** array of integers `nums`, every element appears twice **except for one**. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

### Example Cases
1. Case 1:
>Input: `nums = [2,2,1]`
>
>Output: 1

2. Case 2:
>Input: `nums = [4,1,2,1,2]`
>
>Output: 4

### Constraints
`1 < = nums.length < = 3 * 10^4`

`-3 * 10^4 < = nums[I] < = 3 * 10^4`

Each element in the array appears twice except for **one element** which appears only once.

---
## Python Solution

```python
def singleNumber(nums):
    result = 0
    for num in nums:
        result ^= num  # XOR operation
    return result
```

---

### Explanation of the Solution

The solution uses the **bitwise XOR operation (`^`)** to find the single number. The XOR operation has the following properties:
1. `x ^ x = 0` (Any number XORed with itself is 0).
2. `x ^ 0 = x` (Any number XORed with 0 remains unchanged).
3. XOR is **commutative** and **associative**, so the order of operations does not matter.

Logic:
- When every number appears twice, their XOR will cancel each other out, leaving only the unique number.
- We initialize `result = 0` and XOR every number in the array with `result`.
- By the end of the loop, `result` will hold the single number.


### Example Walkthrough
**Input:**
```python
nums = [5, 3, 1, 3, 5]
```

1. **Initial State**:
   - `result = 0`

2. **Iterate Through `nums`**:
   - `result = 0 ^ 5 = 5`  (First element)
   - `result = 5 ^ 3 = 6`  (Second element)
   - `result = 6 ^ 1 = 7`  (Third element)
   - `result = 7 ^ 3 = 4`  (Fourth element)
   - `result = 4 ^ 5 = 1`  (Fifth element)

3. **Final Result**:
   - `result = 1`

**Output:** `1`
