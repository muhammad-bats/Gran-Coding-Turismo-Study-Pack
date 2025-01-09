# Example Problem 3: Can Place Flowers

## Problem Statement
You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in **adjacent** plots.

Given an integer array `flowerbed` containing `0`'s and `1`'s, where `0` means empty and `1` means not empty, and an integer `n`, return `true` *if `n` new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule and `false` otherwise*.

### Example Cases
1. Case 1:
>Input: `flowerbed = [1,0,0,0,1]`, `n = 1`
>
>Output: true
>
>Explanation: After placing flower, `flowerbed = [1, 0, 1, 0, 1]`

2. Case 2:
>Input: `flowerbed = [1,0,0,0,1]`, `n = 2`
>
>Output: false
>
>Explanation: 2 flowers cannot be placdd without violating the no-adjacent rule

### Constraints
`1 < = flowerbed.length < = 2 * 10^4`

`flowerbed[i]` is `0` or `1`.

There are no two adjacent flowers in flowerbed.

`0 < = n < = flowerbed.length`

---
## Python Solution

```python
def canPlaceFlowers(flowerbed, n):
    count = 0
    length = len(flowerbed)
    
    for i in range(length):
        if flowerbed[i] == 0:  # Check if current plot is empty
            # Check if the left and right plots are empty or boundaries
            prev_empty = (i == 0) or (flowerbed[i - 1] == 0)
            next_empty = (i == length - 1) or (flowerbed[i + 1] == 0)
            
            if prev_empty and next_empty:
                flowerbed[i] = 1  # Plant a flower here
                count += 1
                if count >= n:
                    return True
    
    return count >= n
```

---

### Explanation of the Solution

1. **Iterate Through the Flowerbed**:
   - Traverse the flowerbed array to find positions where flowers can be planted.

2. **Check Planting Conditions**:
   - A flower can be planted if:
     - The current plot is empty (`flowerbed[i] == 0`).
     - The left plot is either empty or out of bounds (`i == 0` or `flowerbed[i-1] == 0`).
     - The right plot is either empty or out of bounds (`i == len(flowerbed)-1` or `flowerbed[i+1] == 0`).

3. **Update the Flowerbed**:
   - Once a flower is planted, mark the plot as occupied (`flowerbed[i] = 1`) to ensure no adjacent planting.

4. **Early Termination**:
   - If the number of planted flowers reaches or exceeds `n`, return `True` immediately.

5. **Final Check**:
   - If the loop completes and fewer than `n` flowers have been planted, return `False`.

### Example Walkthrough

**Input:**
```plaintext
flowerbed = [0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0]
n = 2
```
1. **Initial Flowerbed**:
   ```plaintext
   [0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0]
   ```

2. **Traverse Flowerbed**:
   - Index 0: Empty plot, but adjacent plot is occupied. Skip.
   - Index 1: Occupied plot. Skip.
   - Index 2: Empty plot, but adjacent plot is occupied. Skip.
   - Index 3: Empty plot, but adjacent plot is occupied. Skip
   - Index 4 to 6: Occupied or adjacent plots occupied. Skip.
   - Index 7: Empty plot, both adjacent plots are empty. Plant a flower here.
     ```plaintext
     [0, 1, 0, 1, 1, 0, 1, 1, 0, 0, 1, 0]
     ```
     `count = 1`

3. **Check Count**:
   - `count = 1`, which does not equal `n`. Return `False`.

**Output:** `False`
