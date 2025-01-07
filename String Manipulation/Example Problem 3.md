# Example Problem 3: Generate Parentheses

## Problem Statement
Given `n` pairs of parentheses, write a function to generate all combinations of *well-formed* parentheses.

### Example Cases
1. Case 1:
>Input: n = 3
>
>Output: ```[ "((()))" , "(()())" , "(())()" , "()(())"  ]```

2. Case 2:
>Input: n = 1
>
>Output: ```[ "()" ]```

3. Case 3:
>Input: n = 2
>
>Output: ```[ "(())" , "()()" ]```

### Constraints
`1 < = n < = 5`

---
## Python Solution
```python
def generateParentheses(n):
    def backtrack(current, open_count, close_count):
        # Base case: when the current string has 2 * n characters
        if len(current) == 2 * n:
            result.append(current)
            return
        
        # Add an open parenthesis if we haven't used all 'n' open ones
        if open_count < n:
            backtrack(current + "(", open_count + 1, close_count)
        
        # Add a close parenthesis if the number of close ones is less than open ones
        if close_count < open_count:
            backtrack(current + ")", open_count, close_count + 1)
    
    result = []
    backtrack("", 0, 0)
    return result

# Example usage
n = 3
print(generateParentheses(n))
```
---
## Explanation of the Solution
1. **Recursive Backtracking:**
   - The function `backtrack` is a helper function that recursively generates all valid combinations.
   - It keeps track of:
     - `current`: The current string being built.
     - `open_count`: Number of open parentheses used.
     - `close_count`: Number of close parentheses used.

2. **Base Case:**
   - When the length of `current` equals `2 * n` (the total number of characters in a valid combination for `n` pairs), we add it to the `result` list.

3. **Decision Point:**
   - Add an open parenthesis `(` if `open_count < n`.
   - Add a close parenthesis `)` if `close_count < open_count`.

4. **Result:**
   - The function returns a list of all valid combinations of parentheses.
  
### Example Walkthrough
**Input:** 3
- Start with an empty string (`current = ""`), `open_count = 0`, `close_count = 0`.
- Add `(` (since `open_count < n`):
  - `current = "(", open_count = 1, close_count = 0.`
- Add another `(`:
  - `current = "((", open_count = 2, close_count = 0.`
- Add another `(`:
  - `current = "(((", open_count = 3, close_count = 0.`
- Add `)` (since `close_count < open_count`):
  - `current = "((()", open_count = 3, close_count = 1.`
- Add another `)`:
  - `current = "((())", open_count = 3, close_count = 2.`
- Add another `)`:
  - `current = "((()))", open_count = 3, close_count = 3.`
  - This is a valid combination since `len(current) = 2 * n`. Add to `result.`
- Backtrack and try other combinations:
  - For example, after exploring `"((()))"`, try replacing one of the `(` with a `)` earlier.

**Output:** ```["((()))", "(()())", "(())()", "()(())", "()()()"]```
