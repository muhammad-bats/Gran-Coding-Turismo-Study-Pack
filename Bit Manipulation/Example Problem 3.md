# Example Problem 3: Reverse Bits

## Problem Statement
Reverse bits of a given 32 bits unsigned integer.

### Example Cases
1. Case 1:
>Input: n = **00000010100101000001111010011100**
>
>Output:    964176192 (**00111001011110000010100101000000**)
>
>Explanation: The input binary string **00000010100101000001111010011100** represents the unsigned integer 43261596, so return 964176192 which its binary representation is **00111001011110000010100101000000**.

2. Case 2:
>Input: n = **11111111111111111111111111111101**
>
>Output:   3221225471 (10111111111111111111111111111111)
>
>Explanation: The input binary string **11111111111111111111111111111101** represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is **10111111111111111111111111111111**.

### Constraints
The input must be a **binary string** of length `32`.

---
## Python Solution

```python
def reverseBits(n: int) -> int:
    result = 0
    for _ in range(32):  # Since it is a 32-bit integer
        result = (result << 1) | (n & 1)  # Shift result left and add the last bit of n
        n >>= 1  # Shift n right to process the next bit
    return result
```

---

### Explanation of the Solution

1. **Key Idea**:
   - The goal is to reverse the bits of a 32-bit unsigned integer.
   - Starting with an empty result, iterate through all 32 bits of the input integer.
   - In each iteration:
     1. Left shift the result to make room for the new bit.
     2. Extract the last bit of `n` using `n & 1` and add it to the result using bitwise OR.
     3. Right shift `n` by 1 to process the next bit.

2. **Bit Manipulation**:
   - `result = (result << 1)`: Shifts all bits of `result` to the left, making space for the next bit.
   - `(n & 1)`: Extracts the last bit of `n`.
   - `|`: Combines the shifted `result` with the new bit.
   - `n >>= 1`: Moves the bits of `n` to the right, effectively removing the last processed bit.


### Example Walkthrough

**Input**:  
```
n = 10101011100011110000111101010101
```

1. Start with `result = 0` and `n = 10101011100011110000111101010101`.
2. Process each bit of `n` from right to left:
   - Iteration 1: `result = 1`, `n = 1010101110001111000011110101010`.
   - Iteration 2: `result = 10`, `n = 101010111000111100001111010101`.
   - Iteration 3: `result = 101`, `n = 10101011100011110000111101010`.
   - ...
   - Iteration 32: `result = 10101011111100001111000111010101`, `n = 0`.

3. Final reversed binary:
   ```
   10101011111100001111000111010101
   ```

**Output**:  ` 2874540205 # as binary: 10101011111100001111000111010101 `
