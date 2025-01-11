# Example Problem 1: Diamond Number Pattern

## Problem Statement
for a given integer `n` (number of rows in the top half of the diamond) print the following diamond number pattern: 

For example, for `n = 4`, the output should look like this:
```
   1
  121
 12321
1234321
 12321
  121
   1
```

Each row in the diamond consists of increasing numbers from `1` to the row number, followed by decreasing numbers back to `1`. The pattern is symmetric about its center.

### Example Cases

1. Case 1:
>Input:
>```
>n = 4
>```
>
>Output:
>  ```
>     1
>    121
>   12321
>  1234321
>   12321
>    121
>     1
>  ```
>
>Explanation:  
>The diamond pattern for `n = 4` starts with a single `1` at the center. The rows above and below increase and decrease symmetrically, creating a diamond shape.

2. Case 2:
>Input:
>```
>n = 3
>```
>
>Output:
>  ```
>    1
>   121
>  12321
>   121
>    1
>  ```
>
>Explanation:  
>For `n = 3`, the diamond has three rows in the top half, including the widest row. The bottom rows mirror the top rows.

### Constraints
`1 < = n < = 50`

The input `n` should be a positive integer.

The output must follow the diamond pattern, ensuring proper alignment with spaces.

---

## Python Solution
```python
def diamond_number_pattern(n):
    # Top half of the diamond
    for i in range(1, n + 1):
        # Print spaces
        print(" " * (n - i), end="")
        # Print increasing numbers
        for j in range(1, i + 1):
            print(j, end="")
        # Print decreasing numbers
        for j in range(i - 1, 0, -1):
            print(j, end="")
        print()  # New line after each row
    
    # Bottom half of the diamond
    for i in range(n - 1, 0, -1):
        # Print spaces
        print(" " * (n - i), end="")
        # Print increasing numbers
        for j in range(1, i + 1):
            print(j, end="")
        # Print decreasing numbers
        for j in range(i - 1, 0, -1):
            print(j, end="")
        print()  # New line after each row
```

---

### Explanation of the Solution
The solution constructs the diamond pattern in two parts: the top half and the bottom half. 

1. **Top Half Construction:**
   - The loop iterates from `1` to `n`. For each row:
     - Spaces are printed to align the numbers centrally (`n - i` spaces for row `i`).
     - Numbers are printed in an increasing order from `1` to `i`.
     - Numbers are printed in a decreasing order from `i-1` back to `1`.

2. **Bottom Half Construction:**
   - The loop iterates from `n-1` to `1`. For each row:
     - Spaces are printed for alignment.
     - Numbers are printed in increasing and decreasing orders similar to the top half.

3. The `end=""` in `print()` is used to control the placement of spaces and numbers within the same line.

### Example Walkthrough
**Input:**
```
n = 5
```

1. **Top Half:**
   - Row 1: Spaces: `4`, Numbers: `1`
   - Row 2: Spaces: `3`, Numbers: `121`
   - Row 3: Spaces: `2`, Numbers: `12321`
   - Row 4: Spaces: `1`, Numbers: `1234321`
   - Row 5: Spaces: `0`, Numbers: `123454321`

2. **Bottom Half:**
   - Row 4 (mirrored): Spaces: `1`, Numbers: `1234321`
   - Row 3 (mirrored): Spaces: `2`, Numbers: `12321`
   - Row 2 (mirrored): Spaces: `3`, Numbers: `121`
   - Row 1 (mirrored): Spaces: `4`, Numbers: `1`

**Output:**
```
    1
   121
  12321
 1234321
123454321
 1234321
  12321
   121
    1
```
