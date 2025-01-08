# Example Problem 5: Maximum Points on a Line

## Problem Statement
Given an array of points where `points[i] = [xi, yi]` represents a point on the **X-Y** plane, return *the maximum number of points that lie on the same straight line.*

### Example Cases
1. Case 1:
---

<div align="center">
  <img src="https://github.com/user-attachments/assets/1af7b1cf-582d-498c-bc93-765e362ac1a4" width="350"> 
</div>

---
>Input: points = `[[1,1],[2,2],[3,3]]`
>
>Output: 3

2. Case 2:
---

<div align="center">
  <img src="https://github.com/user-attachments/assets/320b6721-d47d-4b73-80bc-3e36d299b60e" width="350"> 
</div>

---
>Input: points = `[[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]`
>
>Output: 4

### Constraints
`1 < = points.length < = 300`

`points[i].length == 2`

`-10^4 < = xi, yi < = 10^4`

All the points are **unique**.

---

## Python Solution
```python
from collections import defaultdict
from math import gcd

def max_points(points):
    if len(points) <= 2:
        return len(points)
    
    def get_slope(p1, p2):
        dx = p2[0] - p1[0]
        dy = p2[1] - p1[1]
        if dx == 0:  # vertical line
            return (float('inf'), 0)
        if dy == 0:  # horizontal line
            return (0, float('inf'))
        g = gcd(dx, dy)
        return (dy // g, dx // g)
    
    max_count = 0
    
    for i in range(len(points)):
        slopes = defaultdict(int)
        duplicate = 1
        for j in range(i + 1, len(points)):
            if points[i] == points[j]:
                duplicate += 1
            else:
                slope = get_slope(points[i], points[j])
                slopes[slope] += 1
        max_count = max(max_count, duplicate + max(slopes.values(), default=0))
    
    return max_count
```
---

### Explanation of the Solution
1. **Edge Case**:
   - If there are `< = 2` points, they all lie on the same line, so the result is the number of points.
2. **Using Slopes to Identify Lines**:
   - A line can be uniquely defined by its slope `m`, calculated as `m` = y<sub>2</sub> - y<sub>1</sub> // x<sub>2</sub> - x<sub>1</sub>`.
   - To avoid floating-point errors, store slopes as reduced fractions using the greatest common divisor (GCD).

3. **Vertical and Horizontal Lines**:
   - Vertical lines have an infinite slope `dx = 0`.
   - Horizontal lines have a zero slope `dy = 0`.
4. **Using a Dictionary for Counting Slopes**:
   - For each point `i`, iterate over all other points `j` and compute the slope between `i` and `j`.
   - Store these slopes in a dictionary `slopes` to count how many points share the same slope with `i`.
5. **Handling Duplicate Points**:
   - If two points are identical, count them as duplicates to add them to the total line count later.
6. **Track the Maximum Points on a Line**:
   - For each point `i`, calculate the maximum number of points on a line passing through `i`, considering slopes and duplicates.
7. **Return the Result**:
   - After processing all points, return the maximum count.

### Example Walkthrough
**Input:**
```python
points = [[1, 1], [2, 2], [3, 3], [3, 1]]
```

#### Step-by-Step Execution:
1. Start with `i = 0`, point `[1, 1]`:
   - Compare with `[2, 2]`: slope = `(1, 1)` (normalized using GCD).
   - Compare with `[3, 3]`: slope = `(1, 1)`.
   - Compare with `[3, 1]`: slope = `(0, ♾️)` (horizontal line).
   - Slopes: `{(1, 1): 2, (0, ♾️): 1}`.
   - Maximum points for `[1, 1]`: 1 + max(2, 1) = 3.

2. i = 1`, point `[2, 2]`:
   - Compare with `[3, 3]`: slope = `(1, 1)`.
   - Compare with `[3, 1]`: slope = `(-1, 1)`.
   - Slopes: `{(1, 1): 1, (-1, 1): 1}`.
   - Maximum points for `[2, 2]`: 1 + max(1, 1) = 2.

3. `i = 2`, point `[3, 3]`:
   - Compare with `[3, 1]`: slope = `(0, ♾️)`.
   - Slopes: `{(0, ♾️): 1}`.
   - Maximum points for `[3, 3]`: 1 + max(1) = 2.

4. Final result:
   - The maximum number of points on the same line is **3**.

**Output:** 3
