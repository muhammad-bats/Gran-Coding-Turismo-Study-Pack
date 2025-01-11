# Example Problem 4: Spiral Number Pattern

## Problem Statement
generate a clockwise spiral pattern of numbers for a given `n`, where `n` represents the size of a square matrix. The numbers start from `1` and increment sequentially as they spiral inward.

### Example Cases
1. Case 1:
>Input:  
>```
>n = 3
>```
>
>Output:  
>```
>1   2   3
>8   9   4
>7   6   5
>```

2. Case 2:
>Input:  
>```
>n = 5
>```
>
>Output:  
>```
>1   2   3   4   5
>16  17  18  19   6
>15  24  25  20   7
>14  23  22  21   8
>13  12  11  10   9
>```

### Constraints
`1 < = n < = 50`.

Input `n` is a positive integer.

## Python Solution
```python
def generate_spiral_matrix(n):
    # Initialize an empty n x n matrix with 0s
    matrix = [[0 for _ in range(n)] for _ in range(n)]
    
    # Initialize variables
    num = 1  # Start filling with 1
    top, bottom = 0, n - 1  # Row boundaries
    left, right = 0, n - 1  # Column boundaries

    # Fill the matrix in a spiral order
    while top <= bottom and left <= right:
        # Fill top row (left to right)
        for col in range(left, right + 1):
            matrix[top][col] = num
            num += 1
        top += 1

        # Fill right column (top to bottom)
        for row in range(top, bottom + 1):
            matrix[row][right] = num
            num += 1
        right -= 1

        # Fill bottom row (right to left)
        if top <= bottom:
            for col in range(right, left - 1, -1):
                matrix[bottom][col] = num
                num += 1
            bottom -= 1

        # Fill left column (bottom to top)
        if left <= right:
            for row in range(bottom, top - 1, -1):
                matrix[row][left] = num
                num += 1
            left += 1

    return matrix

def print_spiral_matrix(matrix):
    for row in matrix:
        print("   ".join(map(str, row)))

# Example usage
n = int(input("Enter the size of the matrix: "))
spiral_matrix = generate_spiral_matrix(n)
print_spiral_matrix(spiral_matrix)
```

---

### Explanation of the Solution

1. **Matrix Initialization:**
   - Create an `n * n` matrix initialized with zeros.

2. **Boundary Variables:**
   - Use `top`, `bottom`, `left`, and `right` to define the current boundaries of the matrix to fill numbers.

3. **Filling Logic:**
   - Fill the matrix layer by layer in a clockwise spiral:
     - **Top Row:** Left to right within current bounds.
     - **Right Column:** Top to bottom within current bounds.
     - **Bottom Row:** Right to left within current bounds (if applicable).
     - **Left Column:** Bottom to top within current bounds (if applicable).

4. **Update Boundaries:**
   - Narrow the boundaries (`top`, `bottom`, `left`, `right`) after filling each layer.

5. **Final Output:**
   - Print the `n * n` matrix row by row.

### EXample Walkthrough

**Input:**
```
n = 4
```

1. **Initialization:**
   - `n = 4`, create a `4 * 4` matrix filled with zeros.
   - Boundaries: `top = 0`, `bottom = 3`, `left = 0`, `right = 3`.

2. **First Iteration:**
   - **Top Row:** Fill `[1, 2, 3, 4]`.
   - Update `top = 1`.

3. **Second Iteration:**
   - **Right Column:** Fill `[5, 6, 7]`.
   - Update `right = 2`.

4. **Third Iteration:**
   - **Bottom Row:** Fill `[8, 9, 10]`.
   - Update `bottom = 2`.

5. **Fourth Iteration:**
   - **Left Column:** Fill `[11, 12]`.
   - Update `left = 1`.

6. **Filling Inner Layer:**
   - Fill inner numbers sequentially: `[13, 14, 15, 16]`.

**Output:**
```
1   2   3   4
12  13  14   5
11  16  15   6
10   9   8   7
```
