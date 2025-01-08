# Example Problem 4: Ugly Number

## Problem Statement
An **ugly number** is a *positive* integer which does not have a prime factor other than `2`, `3`, and `5`.

Given an integer `n`, return `true` if n is an **ugly number**.

### Example Cases
1. Case 1:
>Input: n = 6
>
>Output: true
>
>Explanation: 6 = 2 × 3

2. Case 2:
>Input: n = 1
>
>Output: true
>
>Explanation: 1 has no prime factors.

3. Case 3:
>Input: n = 14
>
>Output: false
>
>Explanation: 14 is not ugly since it includes the prime factor 7.

### Constraints
`-2^31 < = n < = 2^31 - 1`

---
## Python Solutions
```python
def is_ugly(n):
    if n <= 0:
        return False
    
    for factor in [2, 3, 5]:
        while n % factor == 0:
            n //= factor
    
    return n == 1
```
---

### Explanation of the Solution
1. **Handle Negative Numbers and Zero**:
   - Ugly numbers are **positive integers**, so if `n < = 0`, the result is immediately `False`.
2. **Prime Factors `2, 3, 5`**:
   - Repeatedly divide `n` by `2`, `3`, and `5` as long as it is divisible by these numbers. This reduces `n` to its remaining prime factors.
3. **Check the Result**:
   - After dividing out all occurrences of `2`, `3`, and `5`, if `n` becomes `1`, then `n` is an ugly number.
   - If `n` is greater than `1` at the end, it means there are other prime factors, so `n` is not an ugly number.

### Example Walkthrough
**Input:** `n = 189`
1. Check divisibility by `2`:
   - `189 mod 2 < = 0`, so it is not divisible by `2`.
2. Check divisibility by `3`:
   - `189 mod 3 < = 0`, so divide `189` by `3`: `189 div 3 = 63`.
   - `63 mod 3 < = 0`, so divide `63` by `3`: `63 div 3 = 21`.
   - `21 mod 3 = 0`, so divide `21` by `3`: `21 div 3 = 7`.
3. Check divisibility by `5`:
   - `7 mod 5 < = 0`, so it is not divisible by `5`.
4. Remaining `n = 7`, which is not `1`, so `189` is **not** an ugly number.

**Output**: `False`
