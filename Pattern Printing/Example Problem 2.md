# Example Problem: 2 Reverse Pyramid Number Pattern

## Problem Statement
for a given integer `n` (number of rows in the pyramid) print a **reverse pyramid pattern** of numbers. Each row contains numbers in increasing order from `1` to the current row number, followed by decreasing numbers back to `1`. 

For example, for `n = 4`, the pattern should look like:

```
1234321
 12321
  121
   1
```

### Example Cases

1. Case1:
>Input:
>```
>n = 4
>```
>
Output:
>  ```
>  1234321
>   12321
>    121
>     1
>  ```
>
>Explanation:  
>The reverse pyramid has `4` rows.  
> - Row 1 contains `1234321` (no leading spaces).  
> - Row 2 contains `12321` (1 leading space).  
> - Row 3 contains `121` (2 leading spaces).  
> - Row 4 contains `1` (3 leading spaces).  

2. Case 2:
>Input:
>```
>n = 5
>```
>
>Output:
>  ```
>  123454321
>   1234321
>    12321
>     121
>      1
>  ```
>
>Explanation:  
>The reverse pyramid has `5` rows.  
> - Row 1 contains `123454321` (no leading spaces).  
> - Row 2 contains `1234321` (1 leading space).  
> - Row 3 contains `12321` (2 leading spaces).  
> - Row 4 contains `121` (3 leading spaces).  
> - Row 5 contains `1` (4 leading spaces).  

### Constraints
`1 < = n < = 20`

The input `n` should be a positive integer.

---

## Python Solution

```python
def reverse_pyramid_pattern(n):
    for i in range(n, 0, -1):
        # Print leading spaces
        print(" " * (n - i), end="")
        
        # Print increasing numbers
        for j in range(1, i + 1):
            print(j, end="")
        
        # Print decreasing numbers
        for j in range(i - 1, 0, -1):
            print(j, end="")
        
        # Move to the next row
        print()
```

---

### Explanation of the Solution
The solution constructs the reverse pyramid pattern by iterating from `n` (the top row) down to `1` (the bottom row). Each row consists of three main parts:
1. **Leading Spaces:**  
   For each row `i`, there are `n - i` leading spaces to align the numbers correctly.  
   Example: For `n = 4`, Row 1 has `0` spaces, Row 2 has `1` space, and so on.

2. **Increasing Numbers:**  
   From `1` to `i`. This is implemented using a loop from `1` to `i + 1`.

3. **Decreasing Numbers:**  
   From `i - 1` back to `1`. This is implemented using a loop from `i - 1` to `0`.

The pattern is printed row by row, and the `end=""` in the `print()` statement ensures proper placement of numbers and spaces in the same line.

### Example Walkthrough

**Input:**
```
n = 9
```

- **Row 1 (`i = 9`):**
  - Spaces: `n - i = 9 - 9 = 0` → `""`  
  - Increasing Numbers: `123456789`  
  - Decreasing Numbers: `87654321`  
  - Combined Row: `12345678987654321`

- **Row 2 (`i = 8`):**
  - Spaces: `n - i = 9 - 8 = 1` → `" "`  
  - Increasing Numbers: `12345678`  
  - Decreasing Numbers: `7654321`  
  - Combined Row: `" 123456787654321"`

- **Row 3 (`i = 7`):**
  - Spaces: `n - i = 9 - 7 = 2` → `"  "`  
  - Increasing Numbers: `1234567`  
  - Decreasing Numbers: `654321`  
  - Combined Row: `"  1234567654321"`

- **Row 4 (`i = 6`):**
  - Spaces: `n - i = 9 - 6 = 3` → `"   "`  
  - Increasing Numbers: `123456`  
  - Decreasing Numbers: `54321`  
  - Combined Row: `"   12345654321"`

- **Row 5 (`i = 5`):**
  - Spaces: `n - i = 9 - 5 = 4` → `"    "`  
  - Increasing Numbers: `12345`  
  - Decreasing Numbers: `4321`  
  - Combined Row: `"    123454321"`

- **Row 6 (`i = 4`):**
  - Spaces: `n - i = 9 - 4 = 5` → `"     "`  
  - Increasing Numbers: `1234`  
  - Decreasing Numbers: `321`  
  - Combined Row: `"     1234321"`

- **Row 7 (`i = 3`):**
  - Spaces: `n - i = 9 - 3 = 6` → `"      "`  
  - Increasing Numbers: `123`  
  - Decreasing Numbers: `21`  
  - Combined Row: `"      12321"`

- **Row 8 (`i = 2`):**
  - Spaces: `n - i = 9 - 2 = 7` → `"       "`  
  - Increasing Numbers: `12`  
  - Decreasing Numbers: `1`  
  - Combined Row: `"       121"`

- **Row 9 (`i = 1`):**
  - Spaces: `n - i = 9 - 1 = 8` → `"        "`  
  - Increasing Numbers: `1`  
  - Decreasing Numbers: None  
  - Combined Row: `"        1"`

**Output:**
```
12345678987654321
 123456787654321
  1234567654321
   12345654321
    123454321
     1234321
      12321
       121
        1
```
