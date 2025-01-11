### Problem Statement: X-Pattern

given an odd integer `n`, generate an "X" pattern of size `n * n`. The diagonal lines of the "X" are formed by `*` symbols, intersecting at the center of the square.  

### Example Cases
1. Case 1:
>Input: n = 3
>
>Output:
>  ```
>  *   *
>    *
>  *   *
>  ```
>Explanation:
>3 * 3 = 9

2. Case 2:
>Input: n = 5
>
>Output:
> 
>  ```
>  *   *
>   * * 
>    *  
>   * * 
>  *   *
>  ```


### Constraints:
`n` must be an **odd integer**.

`1 < = n < = 50`.

---

## Python Solution:
```python
def print_x_pattern(n):
    # Validate input (odd and within range)
    if n < 1 or n > 49 or n % 2 == 0:
        print("Invalid input. Please enter an odd integer between 1 and 49.")
        return
    
    # Generate the X-pattern
    for i in range(n):
        for j in range(n):
            if j == i or j == n - i - 1:
                print("*", end="")
            else:
                print(" ", end="")
        print()  # Move to the next row

# Example usage
n = int(input("Enter an odd integer (1 ≤ n ≤ 49): "))
print_x_pattern(n)
```

---

### Explanation of the Solution:

1. **Input Validation:**
   - Ensure `n` is an odd integer within the valid range `1 < = n < = 49`.

2. **Pattern Construction:**
   - The "X" pattern is defined by two diagonals:
     - **Primary diagonal:** Characters where `j == i` (top-left to bottom-right).
     - **Secondary diagonal:** Characters where `j == n - i - 1` (top-right to bottom-left).

3. **Logic:**
   - Use nested loops:
     - Outer loop iterates over the rows (`i`).
     - Inner loop iterates over the columns (`j`).
     - Print a `*` if `j == i` or `j == n - i - 1`; otherwise, print a space.
   - After printing each row, move to the next line.


### Example Walkthrough:

**Input:**
```
n = 9
```

1. **Row 1 (`i = 0`):**
   - Print `*` at column `j = 0` (primary diagonal).
   - Print `*` at column `j = 8` (secondary diagonal).

2. **Row 2 (`i = 1`):**
   - Print `*` at column `j = 1` (primary diagonal).
   - Print `*` at column `j = 7` (secondary diagonal).

3. **Row 3 (`i = 2`):**
   - Print `*` at column `j = 2` (primary diagonal).
   - Print `*` at column `j = 6` (secondary diagonal).

4. **Row 4 (`i = 3`):**
   - Print `*` at column `j = 3` (primary diagonal).
   - Print `*` at column `j = 5` (secondary diagonal).

5. **Row 5 (`i = 4`):**
   - Print `*` at column `j = 4` (center intersection).

6. Continue this pattern until **Row 9 (`i = 8`)**, where the same logic applies.

**Output:**
```
*       *
 *     * 
  *   *  
   * *   
    *    
   * *   
  *   *  
 *     * 
*       *
```
