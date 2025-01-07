# Example Problem 4: Palindrome Test

## Problem Statement
A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

### Task
Given a string `s`, return `true` if it is a **palindrome**, or `false` otherwise.

### Example Cases
1. Case 1:
>Input: s = "A man, a plan, a canal: Panama"
>
>Output: true
>
>Explanation: "amanaplanacanalpanama" is a palindrome.

2. Case 2:
>Input: s = "race a car"
>
>Output: false
>
>Explanation: "raceacar" is not a palindrome.

3. Case 3:
>Input: s = " "
>
>Output: true
>
>Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

### Constraints
`1 < = s.length < = 2 * 10^4`

`s` consists only of **printable ASCII** characters.

---
## Python Solution
```python
def isPalindrome(s):
    # Step 1: Clean the string
    cleaned_string = ''.join(char.lower() for char in s if char.isalnum())
    
    # Step 2: Check if the cleaned string is a palindrome
    return cleaned_string == cleaned_string[::-1]

# Example Usage
s1 = "Was it a car or a cat I saw?"
s2 = "No lemon, no melon"
s3 = "Hello, World!"
print(isPalindrome(s1))  # Output: True
print(isPalindrome(s2))  # Output: True
print(isPalindrome(s3))  # Output: False
```

---
### Explanation

1. **Step 1: Clean the Input String**
   - Remove all non-alphanumeric characters using `char.isalnum()`.
   - Convert all characters to lowercase using `char.lower()` for uniformity.
   - Combine the remaining characters into a single string using `join`.

2. **Step 2: Check for Palindrome**
   - Compare the cleaned string to its reverse using slicing (`[::-1]`).
   - If the cleaned string matches its reverse, it is a palindrome.

3. **Return the Result**
   - Return `True` if the cleaned string is a palindrome.
   - Otherwise, return `False`.

### Example Walkthrough
**Input:** `s = "No lemon, no melon"`

1. **Clean the String**:
   - Remove non-alphanumeric characters and convert to lowercase:
     - `"Nolemonnomelon"`
   - Result: `"nolemonnomelon"`
2. **Check for Palindrome**:
   - `"nolemonnomelon"` == `"nolemonnomelon"[::-1]` (True)
3. **Output**: `True`
