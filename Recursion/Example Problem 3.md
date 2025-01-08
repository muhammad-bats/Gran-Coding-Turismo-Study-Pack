# Example Problem 3: Pow(x, n)

## Problem Statement
Implement pow(x, n), which calculates `x` raised to the power `n` (i.e., `x^n`).

### Example Cases
1. Case 1:
>Input: x = 2.00000, n = 10
>
>Output: 1024.00000

2. Case 2:
>Input: x = 2.10000, n = 3
>
>Output: 9.26100

3. Case 3:
>Input: x = 2.00000, n = -2
>
>Output: 0.25000
>
>Explanation: 2^(-2) = 1/(2^2) = 1/4 = 0.25

### Constraints
`-100.0 < x < 100.0`

`-2^31 < = n < = 2^31-1`

`n` is an integer.

Either `x` is not zero or `n > 0`.

`-10^4 < = x^n < = 10^4`

---
## Python Solution
```python
def myPow(x: float, n: int) -> float:
    # Base cases
    if n == 0:
        return 1
    if n < 0:
        return 1 / myPow(x, -n)
    
    # Recursive step: split the problem into smaller powers
    half = myPow(x, n // 2)
    if n % 2 == 0:
        return half * half  # If n is even
    else:
        return half * half * x  # If n is odd
```

---

### Explanation of the Solution

1. **Base Cases**:
   - If `n == 0`: Any number raised to the power of `0` is `1`.
   - If `n < 0`: The result is the reciprocal of `x^-n`, i.e., `1 / pow(x, -n)`.

2. **Recursive Step**:
   - Divide the problem into smaller subproblems by halving `n`:
     - Calculate `myPow(x, n // 2)` to reduce computation.
   - If `n` is **even**, `x^n = (x^(n/2)) * (x^(n/2))` (e.g., `2^4 = 2^2 * 2^2`).
   - If `n` is **odd**, `x^n = (x^(n//2)) * (x^(n//2)) * x` (e.g., `2^3 = 2^1 * 2^1 * 2`).

3. **Efficiency**:
   - The recursive algorithm reduces the time complexity to **O(log n)** by halving `n` at each step.

### Example Walkthrough
**Input:** `x = 2.00000, n = 10`
1. Start: `myPow(2, 10)`
   - `n` is not 0 or negative, so proceed.
   - Halve `n`: Call `myPow(2, 5)`.
2. Call: `myPow(2, 5)`
   - `n` is odd, so proceed.
   - Halve `n`: Call `myPow(2, 2)`.
3. Call: `myPow(2, 2)`
   - `n` is even, so proceed.
   - Halve `n`: Call `myPow(2, 1)`.
4. Call: `myPow(2, 1)`
   - `n` is odd, so proceed.
   - Halve `n`: Call `myPow(2, 0)`.
5. Call: `myPow(2, 0)`
   - Base case: Return `1`.
6. Backtrack:
   - `myPow(2, 1)`: `1 * 1 * 2 = 2`.
   - `myPow(2, 2)`: `2 * 2 = 4`.
   - `myPow(2, 5)`: `4 * 4 * 2 = 32`.
   - `myPow(2, 10)`: `32 * 32 = 1024`.

**Output:** `1024.00000`
