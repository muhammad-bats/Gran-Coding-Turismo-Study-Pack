# Example Problem 3: Next Greater Element

## Problem Statement
The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right of** `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

*Return an array `ans` of length `nums1.length` such that `ans[i]` is the **next greater element** as described above.*

### Example Cases

1. Case 1:
   > Input: `nums1 = [4,1,2]`, `nums2 = [1,3,4,2]`  
   > Output: `[-1,3,-1]`  
   > Explanation:  
   > - 4 in `nums2 = [1,3,4,2]`. There is no next greater element, so the answer is -1.  
   > - 1 in `nums2 = [1,3,4,2]`. The next greater element is 3.  
   > - 2 in `nums2 = [1,3,4,2]`. There is no next greater element, so the answer is -1.

2. Case 2:
   > Input: `nums1 = [2,4]`, `nums2 = [1,2,3,4]`  
   > Output: `[3,-1]`  
   > Explanation:  
   > - 2 in `nums2 = [1,2,3,4]`. The next greater element is 3.  
   > - 4 in `nums2 = [1,2,3,4]`. There is no next greater element, so the answer is -1.

### Constraints:
`1 < = nums1.length < = nums2.length < = 1000`

`0 < = nums1[i], nums2[I] < = 10^4`

All integers in `nums1` and `nums2` are unique.

All the integers of `nums1` also appear in `nums2`.

---

## Python Solution
```python
def nextGreaterElement(nums1, nums2):
    stack = []
    next_greater_map = {}

    # Traverse nums2 to build a map of the next greater elements
    for num in nums2:
        while stack and stack[-1] < num:
            next_greater_map[stack.pop()] = num
        stack.append(num)

    # For elements that do not have a next greater element
    while stack:
        next_greater_map[stack.pop()] = -1

    # Find the results for nums1 based on the next_greater_map
    return [next_greater_map[num] for num in nums1]
```

---

### Explanation of the Solution
This solution utilizes a **monotonic decreasing stack** to efficiently compute the next greater element for each number in `nums2`:
1. **Initialize Data Structures**: Use a stack to keep track of elements for which the next greater element has not yet been found. Use a dictionary `next_greater_map` to store the next greater element for each number in `nums2`.
2. **Traverse `nums2`**:
   - For each number in `nums2`, check the stack.
   - If the current number is greater than the number on top of the stack, the current number is the next greater element for the top of the stack. Pop the stack and update the map.
   - Push the current number onto the stack.
3. **Handle Remaining Elements**: For numbers still in the stack after traversing `nums2`, assign `-1` as there is no greater element.
4. **Answer for `nums1`**: Use the map to find the next greater elements for all numbers in `nums1`.

### Example Walkthrough
**Input:**  
```
nums1 = [1,3]  
nums2 = [1,3,2,4]
``` 

1. **Building the Next Greater Map:**
   - Start with an empty stack and map: `stack = []`, `next_greater_map = {}`.
   - Traverse `nums2`:
     - Add `1` to the stack: `stack = [1]`.
     - Compare `3` with top of stack (`1`): `3 > 1`. Update `next_greater_map = {1: 3}`. Pop `1`, add `3` to the stack: `stack = [3]`.
     - Add `2` to the stack: `stack = [3, 2]`.
     - Compare `4` with top of stack (`2`): `4 > 2`. Update `next_greater_map = {1: 3, 2: 4}`. Pop `2`.
     - Compare `4` with top of stack (`3`): `4 > 3`. Update `next_greater_map = {1: 3, 2: 4, 3: 4}`. Pop `3`.
     - Add `4` to the stack: `stack = [4]`.
   - Elements left in the stack (`4`) have no greater element. Update `next_greater_map = {1: 3, 2: 4, 3: 4, 4: -1}`.

2. **Building Result for `nums1`:**
   - Use `next_greater_map`: `ans = [next_greater_map[1], next_greater_map[3]] = [3, 4]`.

**Output:**  `[3, 4]`  
