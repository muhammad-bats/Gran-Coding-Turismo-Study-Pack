# Example Problem 5: Reverse Vowels of a String

## Problem Statement
Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`, and they can appear in both lower and upper cases, more than once.

### Example Cases
1. Case 1:
>Input: s = "IceCreAm"
>
>Output: "AceCreIm"
>
>Explanation: The vowels in `s` are `['I', 'e', 'e', 'A']`. On reversing the vowels, `s` becomes "AceCreIm".

2. Case 2:
>Input: s = "Computer"
>
>Output: "Cemputor"
>
>Explanation: The vowels in `s` are `['o', 'u', 'e']`. On reversing the vowels, `s` becomes "Cemputor".

### Constraints
`1 < = s.length < = 3 * 10^4`

`s` consist of **printable ASCII** characters.

---
## Python Solution
```python
def reverseVowels(s):
    # Step 1: Identify vowels
    vowels = set("aeiouAEIOU")
    # Step 2: Convert string to list for mutable operations
    s_list = list(s)
    
    # Step 3: Use two pointers to find vowels and reverse them
    left, right = 0, len(s) - 1
    while left < right:
        # Move left pointer until a vowel is found
        if s_list[left] not in vowels:
            left += 1
        # Move right pointer until a vowel is found
        elif s_list[right] not in vowels:
            right -= 1
        else:
            # Swap the vowels
            s_list[left], s_list[right] = s_list[right], s_list[left]
            left += 1
            right -= 1
    
    # Step 4: Convert the list back to a string
    return ''.join(s_list)

# Example Usage
s1 = "Beaconhouse"
s2 = "Academia"
print(reverseVowels(s1))  # Output: "Beuconhoase"
print(reverseVowels(s2))  # Output: "acidemaA"
```

---

## Explanation of the Solution
1. **Step 1: Identify Vowels**
   - Create a set of vowels `aeiouAEIOU` to efficiently check if a character is a vowel.

2. **Step 2: Convert String to List**
   - Strings in Python are immutable, so converting the string to a list allows us to swap characters.

3. **Step 3: Use Two Pointers**
   - Initialize two pointers: `left` at the start of the string and `right` at the end.
   - Move the `left` pointer forward until it finds a vowel.
   - Move the `right` pointer backward until it finds a vowel.
   - If both pointers point to vowels, swap the vowels, then move the pointers inward.

4. **Step 4: Convert List Back to String**
   - After swapping vowels, convert the list back to a string using `join`.

5. **Return the Result**
   - Return the modified string.

### Example Walkthrough
**Input:** `s = "Academia"`

1. **Initial String**: `"Academia"`
2. **Identify Vowels**: Vowels are `['A', 'a', 'e', 'i', 'a']`.
3. **Pointer Operations**:
   - Swap `A` (at index 0) with `a` (at index 7): `"aceCreIA"`
   - Swap `a` (at index 2) with `i` (at index 6): `"acidemaA"`
4. **Result**: `"acidemaA"`

**Output:** `"acidemaA"`
