# Example Problem 2: Longest Palindrome

## Problem Statement
Given a string `s` which consists of lowercase or uppercase letters, return the length of the **longest palindrome** that can be built with those letters.

Letters are **case sensitive**, for example, `"Aa"` is not considered a palindrome.

### Example Cases
1. Case 1:
>Input: s = "abccccdd"
>
>Output: 7
>
>Explanation: One longest palindrome that can be built is "dccaccd", whose length is 7.

2. Case 2:
>Input: s = "a"
>
>Output: 1
>
>Explanation: The longest palindrome that can be built is "a", whose length is 1.

### Constraints
`1 < = s.length < = 2000`

`s` consists of lowercase and/or uppercase English letters only.

---
## Python Solution

```python
from collections import Counter

def longestPalindrome(s):
    char_count = Counter(s)
    length = 0
    odd_found = False
    
    for count in char_count.values():
        if count % 2 == 0:
            length += count
        else:
            length += count - 1
            odd_found = True
    
    if odd_found:
        length += 1  # Add one odd character to the center of the palindrome
    
    return length
```

---

### Explanation of the Solution

1. **Character Frequency Count**:
   - Use `Counter` from the `collections` module to calculate the frequency of each character in the string.

2. **Building the Palindrome**:
   - For characters with even counts, all of them can be included in the palindrome.
   - For characters with odd counts, use the largest even number of characters (e.g., if a character appears 5 times, include 4).
   - At most, one odd character can be placed in the center of the palindrome.

3. **Final Adjustment**:
   - If there is at least one odd character, add `1` to the length to include it as the center of the palindrome.

### Example Walkthrough

**Input:** `s = "Beaconhouse Notion of Academia"`

1. **Character Frequency**:
   ```
   Counter({
       'o': 5, 'e': 3, 'a': 3, 'n': 3, ' ': 4, 
       'B': 1, 'c': 2, 'h': 1, 'u': 1, 's': 1, 
       'N': 1, 't': 1, 'i': 2, 'f': 1, 'A': 1, 'd': 1, 'm': 1
   })
   ```

2. **Palindrome Length Calculation**:
   - Add all even frequencies:
     - `'o': 4`, `' ': 4`, `'c': 2`, `'i': 2` → Total = `12`
   - Add the largest even part of odd frequencies:
     - `'e': 2`, `'a': 2`, `'n': 2` → Total = `6`
   - Include one odd character as the center (e.g., `'o'`):
     - Total = `12 + 6 + 1 = 19`

**Output**: `19`
