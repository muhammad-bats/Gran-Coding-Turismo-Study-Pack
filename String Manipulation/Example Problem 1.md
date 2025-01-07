# Example Problem 1: Roman to Integer

## Problem Statement
Roman numerals are represented by seven different symbols:

| Symbol | Value |
|--------|-------|
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

For example:
- `II` represents 2 (1 + 1).
- `XII` represents 12 (10 + 2).
- `XXVII` represents 27 (10 + 10 + 5 + 2).

However, in specific cases, subtraction is used instead of addition:
- `IV` represents 4 (5 - 1).
- `IX` represents 9 (10 - 1).
- `XL` represents 40 (50 - 10).
- `XC` represents 90 (100 - 10).
- `CD` represents 400 (500 - 100).
- `CM` represents 900 (1000 - 100).

### Task
Given a Roman numeral string, convert it to an integer.

### Example Cases
1. Case 1:
>Input: s = "III"
>
>Output: 3
>
>Explanation: III = 3.

2. Case 2:
>Input: s = "LVIII"
>
>Output: 58
>
>Explanation: L = 50, V= 5, III = 3.

3. Case 3:
>Input: s = "MCMXCIV"
>
>Output: 1994
>
>Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

### Constraints
`s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.

It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

---

## Python Solution
```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman_to_int = {
            'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000
        }

        total = 0
        prev_value = 0

        for char in reversed(s):
            current_value = roman_to_int[char]

            if current_value < prev_value:
                total -= current_value
            else:
                total += current_value

            prev_value = current_value

        return total

# Example Usage
solver = Solution()
print(solver.romanToInt("III"))   # Output: 3
print(solver.romanToInt("IV"))    # Output: 4
print(solver.romanToInt("IX"))    # Output: 9
print(solver.romanToInt("LVIII")) # Output: 58
print(solver.romanToInt("MCMXCIV")) # Output: 1994
```

---

## Explanation of the Solution
1. **Mapping Roman Symbols to Integers:**
   - Create a dictionary `roman_to_int` that maps Roman numeral symbols to their corresponding integer values.

2. **Iterating in Reverse Order:**
   - To handle subtraction cases (e.g., `IV`), iterate through the string in reverse.
   - Keep track of the previous value using `prev_value`.

3. **Add or Subtract Values:**
   - Compare the current symbol's value (`current_value`) to the `prev_value`.
   - If `current_value < prev_value`, subtract `current_value` from the total (e.g., `IV = 5 - 1`).
   - Otherwise, add `current_value` to the total (e.g., `VI = 5 + 1`).

4. **Return the Total:**
   - After processing all characters, the total contains the integer representation of the Roman numeral.

### Example Walkthrough
**Input:** `"MCMXCIV"`
- Start from the rightmost character `V` (value 5).
- Add `V` to the total (`total = 5`).
- Move to `I` (value 1). Since `1 < 5`, subtract it (`total = 4`).
- Move to `C` (value 100). Since `100 > 1`, add it (`total = 104`).
- Continue this process, handling each character and updating the total.
- Final output: `1994`.
