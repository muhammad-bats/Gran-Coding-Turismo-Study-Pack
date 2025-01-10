# Example Problem 5: Maximum Sum of Circular Subarray

## Problem Statement
Given a **circular integer array** `nums` of length `n`, return *the maximum possible sum of a non-empty subarray of `nums`*.

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A **subarray** may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i < = k1`, `k2 < = j` with `k1 % n == k2 % n`.

### Example Cases
1. Case 1:
   > Input: `nums = [1, -2, 3, -2]`
   > 
   > Output: 3  
   > 
   > Explanation: Subarray [3] has maximum sum 3.

2. Case 2:
   > Input: `nums = [5, -3, 5]`  
   >
   > Output: 10  
   >
   > Explanation: Subarray `[5, 5]` has maximum sum 5 + 5 = 10.

3. Case 3:
   > Input: `nums = [-3, -2, -3]`
   >   
   > Output: -2  
   >
   > Explanation: Subarray [-2] has maximum sum -2.

### Constraints:
`n == nums.length`

`1 < = n < = 3 * 10^4`

`-3 * 10^4 < = nums[I] < = 3 * 10^4`

---

## Python Solution
```python
from collections import deque

def maxSubarraySumCircular(nums):
    n = len(nums)
    
    # Function to compute max subarray sum in a normal array (Kadane's algorithm)
    def maxSubarraySum(arr):
        max_sum = curr_sum = arr[0]
        for num in arr[1:]:
            curr_sum = max(num, curr_sum + num)
            max_sum = max(max_sum, curr_sum)
        return max_sum

    # Calculate total sum and max normal subarray sum
    total_sum = sum(nums)
    max_normal = maxSubarraySum(nums)

    # Edge case: if all numbers are negative, return max_normal
    if max_normal < 0:
        return max_normal

    # Calculate max circular subarray sum
    # Invert the array values to use maxSubarraySum for the minimum subarray sum
    nums_inverted = [-num for num in nums]
    max_circular = total_sum + maxSubarraySum(nums_inverted)

    return max(max_normal, max_circular)
```

---

### Explanation of the Solution
1. **Normal Maximum Subarray Sum**:  
   We first compute the maximum subarray sum for the normal (non-circular) case using Kadane's Algorithm.
   
2. **Total Sum and Inverted Array**:  
   - Compute the total sum of the array.
   - Invert the array values (multiply each by `-1`) to leverage Kadane's Algorithm to compute the minimum subarray sum.

3. **Circular Maximum Subarray Sum**:  
   The circular maximum sum can be calculated as `total_sum - minimum_subarray_sum`, which is equivalent to `total_sum + maxSubarraySum(nums_inverted)`.

4. **Return the Result**:  
   Return the larger of the two: `max_normal` (normal case) or `max_circular` (circular case). Handle the edge case where all numbers are negative.

### Example Walkthrough
**Input:**  `nums = [3, -1, 2, -1]`

1. **Normal Maximum Subarray Sum (`max_normal`)**:  
   - Kadane's Algorithm on `nums`:  
     - `curr_sum = 3, max_sum = 3`  
     - `curr_sum = 2, max_sum = 3`  
     - `curr_sum = 4, max_sum = 4`  
     - `curr_sum = 3, max_sum = 4`  
   - `max_normal = 4`.

2. **Total Sum of Array (`total_sum`)**:  
   - `total_sum = 3 + (-1) + 2 + (-1) = 3`.

3. **Inverted Array (`nums_inverted`)**:  
   - `nums_inverted = [-3, 1, -2, 1]`.

4. **Maximum Subarray Sum of Inverted Array (`min_subarray_sum`)**:  
   - Kadane's Algorithm on `nums_inverted`:  
     - `curr_sum = -3, max_sum = -3`  
     - `curr_sum = 1, max_sum = 1`  
     - `curr_sum = -1, max_sum = 1`  
     - `curr_sum = 1, max_sum = 1`.  
   - `min_subarray_sum = -1`.

5. **Circular Maximum Subarray Sum (`max_circular`)**:  
   - `max_circular = total_sum + min_subarray_sum = 3 + 1 = 4`.

6. **Result**:  
   - `max(max_normal, max_circular) = max(4, 4) = 4`.

**Output:** `4`
