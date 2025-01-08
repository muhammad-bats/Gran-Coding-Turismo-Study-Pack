# Example Problem 5: Find the K-th Character in String Game

## Problem Statement
Muhammad and Abdullah are playing a game. Initially, Alice has a string `word = "a"`.

You are given a **positive** integer `k`.

Now Muhammad will ask Abdullah to perform the following operation **forever**:

Generate a new string by **changing** each character in `word` to its next character in the English alphabet, and **append** it to the original word.
For example, performing the operation on `"c"` generates `"cd"` and performing the operation on `"zb"` generates `"zbac"`.

Return the value of the kth character in `word`, after enough operations have been done for `word` to have at least `k` characters.

Note that the character `'z'` can be changed to `'a'` in the operation.

### Example Cases
1. Case 1:
>Input: k = 5
>
>Output: "b"
>
>Explanation:
>
>Initially, `word = "a"`. We need to do the operation three times:
>
>Generated string is `"b"`, word becomes `"ab"`.
>
>Generated string is `"bc"`, word becomes `"abbc"`.
>
>Generated string is `"bccd"`, word becomes `"abbcbccd"`.

2. Case 2:
>Input: k = 10
>
>Output: "c"
>
>Explanation:
>
>Final generated string is: `"abbcbccdbccdcdde"`

### Constraints
`1 < = k < = 500`

`word = "a"` always. 

---
## Python Solution
```python
def findKthCharacter(k: int) -> str:
    def generate_char(current_char: str) -> str:
        # Returns the "next character" in the English alphabet
        return chr((ord(current_char) - ord('a') + 1) % 26 + ord('a'))

    def helper(word: str, k: int) -> str:
        # Base case: If the current word length >= k, we can directly return the character
        if len(word) >= k:
            return word[k - 1]

        # Generate the "next string" based on the current word
        next_string = "".join(generate_char(char) for char in word)
        new_word = word + next_string

        # Recursive call with the newly generated word
        return helper(new_word, k)

    # Start recursion with the initial word "a"
    return helper("a", k)
```

---

### Explanation of the Solution

1. **Key Observations**:
   - Each character in the word transforms into its "next character" in the alphabet.
   - The result of the transformation is appended to the original word.
   - For example:
     - Starting with `"a"`, the next transformation is `"b"`, resulting in `"ab"`.
     - From `"ab"`, the next transformation is `"bc"`, resulting in `"abbc"`.
     - This process continues.

2. **Recursive Approach**:
   - **Base Case**: If the length of the current `word` is greater than or equal to `k`, we stop and return the `k`-th character.
   - **Recursive Step**: Generate the next string by transforming each character in `word` and appending it to the original `word`. Then, recursively call the helper function with the newly formed `word`.

3. **Character Transformation**:
   - To compute the next character, the ASCII value of the current character is shifted cyclically using:
     ```python
     chr((ord(current_char) - ord('a') + 1) % 26 + ord('a'))
     ```
   - This ensures that `z` wraps around to `a`.

4. **Efficiency**:
   - The recursion continues only until the word's length exceeds `k`. Since the word grows exponentially with each iteration, the recursion depth is logarithmic relative to `k`.

### Example Walkthrough
**Input:** `k = 5`
1. **Initial State**:
   - `word = "a"`
2. **First Operation**:
   - Transform: `"a" → "b"`
   - Append: `"a" + "b" = "ab"`
   - Length: `len("ab") = 2` (not enough, continue recursion)
3. **Second Operation**:
   - Transform: `"ab" → "bc"`
   - Append: `"ab" + "bc" = "abbc"`
   - Length: `len("abbc") = 4` (not enough, continue recursion)
4. **Third Operation**:
   - Transform: `"abbc" → "bccd"`
   - Append: `"abbc" + "bccd" = "abbcbccd"`
   - Length: `len("abbcbccd") = 8` (sufficient, stop recursion)
5. **Result**:
   - Return the `k = 5`th character from `"abbcbccd"`, which is `"b"`.

**Output:** `"b"`
