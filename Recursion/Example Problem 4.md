# Example Problem 4: Dcode String

## Problem Statement
Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `10^5`.

### Example Cases
1. Case 1:
>Input: s = "3[a]2[bc]"
>
>Output: "aaabcbc"

2. Case 2:
>Input: s = "3[a2[c]]"
>
>Output: "accaccacc"

3. Case 3:
>Input: s = "2[abc]3[cd]ef"
>
>Output: "abcabccdcdcdef"

### Constraints
`1 < = s.length < = 30`

`s` consists of lowercase English letters, digits, and square brackets `'[]'`.

`s` is guaranteed to be a valid input.

All the integers in `s` are in the range `[1, 300]`.

---
## Python Solution
```python
def decodeString(s: str) -> str:
    def helper(index: int) -> (str, int):
        decoded = ""
        k = 0  # Multiplier for the current level

        while index < len(s):
            char = s[index]
            
            if char.isdigit():
                # Accumulate the multiplier (e.g., handle "12[a]" where k = 12)
                k = k * 10 + int(char)
            
            elif char == '[':
                # Start a new nested decoding and get its result
                nested_decoded, index = helper(index + 1)
                decoded += k * nested_decoded  # Append the repeated result
                k = 0  # Reset the multiplier after using it
            
            elif char == ']':
                # End of the current nested structure
                return decoded, index
            
            else:
                # Append regular characters
                decoded += char
            
            index += 1
        
        return decoded, index

    # Start recursion from index 0 and return the decoded string
    result, _ = helper(0)
    return result
```

---

### Explanation of the Solution

1. **Helper Function (`helper`)**:
   - This function takes an index as input and processes the string from that point.
   - It handles decoding by maintaining:
     - `decoded`: The partially decoded string for the current level.
     - `k`: The multiplier to repeat the nested string.
2. **Processing Steps**:
   - **Digits (`char.isdigit()`)**: Accumulate the multiplier `k` (e.g., handle cases like `12[a]`).
   - **Opening Bracket (`[`)**: Trigger a recursive call to decode the nested string starting after the `[` character.
   - **Closing Bracket (`]`)**: End the current recursive call and return the decoded string and the updated index.
   - **Letters**: Append regular characters directly to the `decoded` string.
3. **Recursion**:
   - The function processes nested brackets in a depth-first manner, decoding the innermost bracketed structure first and propagating the results outward.
4. **Base Case**:
   - If the helper function reaches the end of the string or encounters a `]`, it stops processing and returns the decoded result for the current level.
5. **Efficiency**:
   - The recursion handles nested structures efficiently by breaking the problem into smaller subproblems.
---

### Example Walkthrough
**Input:** `s = "2[abc]3[cd]ef"`
1. Start: `helper(0)`  
   - `k = 2` (from `2`)
   - Encounter `[`: Call `helper(1)`
2. Nested Call: `helper(1)`  
   - `decoded = "abc"` (from `abc`)
   - Encounter `]`: Return `("abc", 4)`
3. Backtrack:
   - `decoded = "abcabc"` (2 * "abc")
   - `k = 3` (from `3`)
   - Encounter `[`: Call `helper(6)`
4. Nested Call: `helper(6)`  
   - `decoded = "cd"` (from `cd`)
   - Encounter `]`: Return `("cd", 9)`
5. Backtrack:
   - `decoded = "abcabccdcdcd"` (combine results)
   - Append remaining: `decoded = "abcabccdcdcdef"`

**Output:** `"abcabccdcdcdef"`
