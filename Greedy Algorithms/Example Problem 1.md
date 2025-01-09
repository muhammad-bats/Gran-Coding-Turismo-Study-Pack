# Example Problem 1: Container With Most Water

## Problem Statement
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the i<sup>th</sup> line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

*Return the maximum amount of water a container can store.*

**Notice:** that you may not slant the container.

### Example Cases
1. Case 1:
---
<div align="center">
  <img src="https://github.com/user-attachments/assets/f11aa4bf-efaa-4440-8c85-d26ecde9bac9" width="450"> 
</div>

---
>Input: height = `[1,8,6,2,5,4,8,3,7]`
>
>Output: 49
>
>Explanation: The above vertical lines are represented by array `[1,8,6,2,5,4,8,3,7]`. In this case, the max area of water (blue section) the container can contain is `49`.

2. Case 2:
>Input: height = `[1,1]`
>
>Output: 1

### Constraints
`n == height.length`

`2 < = n < = 10^5`

`0 < = height[I] < = 10^4`

---
## Python Solution
```python
def maxArea(height):
    left, right = 0, len(height) - 1
    max_area = 0
    
    while left < right:
        # Calculate the width and current area
        width = right - left
        current_area = width * min(height[left], height[right])
        # Update the maximum area
        max_area = max(max_area, current_area)
        
        # Move the pointer with the smaller height
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    
    return max_area
```

---

### Explanation of the Solution

1. **Two-pointer Approach**:
   - Start with one pointer (`left`) at the beginning of the array and the other (`right`) at the end.
   - The area between the two lines is calculated as `width * min(height[left], height[right])`, where the width is the distance between the two pointers.

2. **Pointer Movement**:
   - To maximize the area, always move the pointer pointing to the shorter line inward. This might increase the height and possibly result in a larger area.

3. **Maximum Area**:
   - Track the maximum area encountered during the iteration.

4. **Stop Condition**:
   - Stop when the two pointers meet.

### Example Walkthrough
**Input:** `height = [4, 7, 1, 3, 8, 11, 2, 6, 1, 4]`
1. **Initial Setup**:
   - `left = 0`, `right = 9`, `max_area = 0`.

2. **Step 1**:
   - Width = `9 - 0 = 9`
   - Height = `min(4, 4) = 4`
   - Area = `9 * 4 = 36`
   - Update `max_area = 36`
   - Move `right` to `8` (since `height[right] <= height[left]`).

3. **Step 2**:
   - Width = `8 - 0 = 8`
   - Height = `min(4, 1) = 1`
   - Area = `8 * 1 = 8`
   - `max_area` remains `36`
   - Move `right` to `7`.

4. **Step 3**:
   - Width = `7 - 0 = 7`
   - Height = `min(4, 6) = 4`
   - Area = `7 * 4 = 28`
   - `max_area` remains `36`
   - Move `left` to `1`.

5. **Step 4**:
   - Width = `7 - 1 = 6`
   - Height = `min(7, 6) = 6`
   - Area = `6 * 6 = 36`
   - `max_area` remains `36`
   - Move `right` to `6`.

6. **Step 5**:
   - Width = `6 - 1 = 5`
   - Height = `min(7, 2) = 2`
   - Area = `5 * 2 = 10`
   - `max_area` remains `36`
   - Move `right` to `5`.

7. **Step 6**:
   - Width = `5 - 1 = 4`
   - Height = `min(7, 11) = 7`
   - Area = `4 * 7 = 28`
   - `max_area` remains `36`
   - Move `left` to `2`.

8. **Step 7**:
   - Width = `5 - 2 = 3`
   - Height = `min(1, 11) = 1`
   - Area = `3 * 1 = 3`
   - `max_area` remains `36`
   - Move `left` to `3`.

9. **Step 8**:
   - Width = `5 - 3 = 2`
   - Height = `min(3, 11) = 3`
   - Area = `2 * 3 = 6`
   - `max_area` remains `36`
   - Move `left` to `4`.

10. **Step 9**:
    - Width = `5 - 4 = 1`
    - Height = `min(8, 11) = 8`
    - Area = `1 * 8 = 8`
    - `max_area` remains `36`
    - Move `left` to `5`.

**Final Result**:
- `max_area = 36`

**Output:** 36
