# Example Problem 4: Maximum Distance in Arrays

## Problem Statement
You are given `m` `arrays`, where each `array` is sorted in **ascending order**.

You can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers `a` and `b` to be their absolute difference `|a - b|`.

*Return the maximum distance.*

### Example Cases
1. Case 1:
>Input: `arrays = [[1,2,3],[4,5],[1,2,3]]`
>
>Output: 4
>
>Explanation: One way to reach the maximum distance 4 is to pick 1 in the first or third array and pick 5 in the second array.

2. Case 2:
>Input: `arrays = [[1],[1]]`
>
>Output: 0
>
>Explanation: `|1 - 1|` is 0

### Constraints
`m == arrays.length`

`2 < = m < = 10^5`

`1 < = arrays[i].length < = 500`

`-10^4 < = arrays[i][j] < = 10^4`

`arrays[i]` is sorted in **ascending order**.

There will be at most `10^5` integers in all the arrays.

---
## Python Solution

```python
def maxDistance(arrays):
    # Initialize min and max values from the first array
    min_val = arrays[0][0]
    max_val = arrays[0][-1]
    max_distance = 0

    # Iterate over arrays starting from the second one
    for i in range(1, len(arrays)):
        # Update the maximum distance based on the current array
        max_distance = max(
            max_distance,
            abs(arrays[i][-1] - min_val),  # Max value of current array vs min value from previous arrays
            abs(max_val - arrays[i][0])   # Min value of current array vs max value from previous arrays
        )

        # Update global min and max values
        min_val = min(min_val, arrays[i][0])
        max_val = max(max_val, arrays[i][-1])

    return max_distance
```

---

### Explanation of the Solution

1. **Tracking Minimum and Maximum**:
   - Maintain the minimum and maximum values encountered so far (`min_val` and `max_val`).

2. **Iterative Comparison**:
   - For each new array, calculate the absolute difference between:
     - The maximum value in the current array and the global minimum (`abs(arrays[i][-1] - min_val)`).
     - The minimum value in the current array and the global maximum (`abs(max_val - arrays[i][0])`).

3. **Update the Maximum Distance**:
   - Update `max_distance` with the larger of the two calculated distances.

4. **Update Global Min and Max**:
   - Adjust `min_val` and `max_val` based on the current array's first and last elements.

5. **Final Result**:
   - After processing all arrays, return the `max_distance`.

### Example Walkthrough

**Input:**
```plaintext
arrays = [[3, 10, 15], [1, 7, 20], [2, 12, 25]]
```

1. **Initialization**:
   ```plaintext
   min_val = 3, max_val = 15, max_distance = 0
   ```

2. **Iterate Over Arrays**:
   - **Second Array `([1, 7, 20])`**:
     - Compare distances:
       ```plaintext
       abs(20 - 3) = 17
       abs(15 - 1) = 14
       ```
     - Update `max_distance`:
       ```plaintext
       max_distance = max(0, 17, 14) = 17
       ```
     - Update `min_val` and `max_val`:
       ```plaintext
       min_val = min(3, 1) = 1
       max_val = max(15, 20) = 20
       ```

   - **Third Array `([2, 12, 25])`**:
     - Compare distances:
       ```plaintext
       abs(25 - 1) = 24
       abs(20 - 2) = 18
       ```
     - Update `max_distance`:
       ```plaintext
       max_distance = max(17, 24, 18) = 24
       ```
     - Update `min_val` and `max_val`:
       ```plaintext
       min_val = min(1, 2) = 1
       max_val = max(20, 25) = 25
       ```

3. **Final Result**:
   ```plaintext
   max_distance = 24
   ```

**Output:** `24`
