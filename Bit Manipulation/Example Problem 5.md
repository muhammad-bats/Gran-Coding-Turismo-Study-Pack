# Example Problem 5: Integer Replacement Game

## Problem Statement
Given a positive integer `n`, you can apply one of the following operations:

1. If `n` is even, replace `n` with `n / 2`.
2. If `n` is odd, replace `n` with either `n + 1` or `n - 1`.
 
*Return the minimum number of operations needed for `n` to become `1`.*

### Example Cases
1. Case 1:
>Input: n = 8
>
>Output: 3
>
>Explanation: 8 → 4 → 2 → 1

2. Case 2:
>Input: n = 7
>
>Output: 4
>
>Explanation: 7 → 8 → 4 → 2 → 1
>
>or 7 → 6 → 3 → 2 → 1

### Constraints
`1 < = n < = 2^31 - 1`

---
## Python Solution

```python
def integerReplacement(n: int) -> int:
    steps = 0
    while n != 1:
        if n % 2 == 0:
            n //= 2
        elif n == 3 or ((n >> 1) & 1) == 0:
            n -= 1
        else:
            n += 1
        steps += 1
    return steps
```

### Explanation of the Solution

The goal is to reduce the integer `n` to `1` with the minimum number of operations. The approach involves:

1. **Dividing by 2 if Even**: If `n` is even, divide it by `2` since this directly halves `n` and minimizes the number of steps.
2. **Increment or Decrement if Odd**:
   - If `n` is odd, decide whether to increment or decrement:
     - Increment (`n + 1`) if it leads to a number with more trailing zeroes in its binary representation. More trailing zeroes mean more divisions by 2 in the future.
     - Decrement (`n - 1`) otherwise.
   - Special case: If `n = 3`, always decrement to avoid an extra step.

This greedy strategy minimizes the number of steps by prioritizing halving whenever possible and strategically incrementing or decrementing when odd.

### Example Walkthrough

**Input:** `n = 25`

1. **Step 1**: `25` is odd → Increment to `26`.
2. **Step 2**: `26` is even → Divide by 2 → `13`.
3. **Step 3**: `13` is odd → Increment to `14`.
4. **Step 4**: `14` is even → Divide by 2 → `7`.
5. **Step 5**: `7` is odd → Increment to `8`.
6. **Step 6**: `8` is even → Divide by 2 → `4`.
7. **Step 7**: `4` is even → Divide by 2 → `2`.
8. **Step 8**: `2` is even → Divide by 2 → `1`.

**Output**: `8`.
