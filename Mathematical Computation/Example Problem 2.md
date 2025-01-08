# Example Problem 2: Integer to Roman

## Problem Statement
Seven different symbols represent Roman numerals with the following values:

| Symbol | Value |
|--------|-------|
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:

- If the value does not start with 4 or 9, select the symbol of the maximal value that can be subtracted from the input, append that symbol to the result, subtract its value, and convert the remainder to a Roman numeral.
- If the value starts with 4 or 9 use the **subtractive form** representing one symbol subtracted from the following symbol, for example, 4 is 1 (`I`) less than 5 (`V`): `IV` and 9 is 1 (`I`) less than 10 (`X`): `IX`. Only the following subtractive forms are used: 4 (`IV`), 9 (`IX`), 40 (`XL`), 90 (`XC`), 400 (`CD`) and 900 (`CM`).
- Only powers of 10 (`I, X, C, M`) can be appended consecutively at most 3 times to represent multiples of 10. You cannot append 5 (`V`), 50 (`L`), or 500 (`D`) multiple times. If you need to append a symbol 4 times use the subtractive form.

### Task
Given an integer, convert it to a Roman numeral.

### Example Cases
1. Case 1:
>Input: num = 3749
>
>Output: `"MMMDCCXLIX"`
>
>Explanation:
>
>3000 = `MMM` as 1000 (`M`) + 1000 (`M`) + 1000 (`M`)
>
> 700 = `DCC` as 500 (`D`) + 100 (`C`) + 100 (`C`)
>
>  40 = `XL` as 10 (`X`) less of 50 (`L`)
>
>   9 = `IX` as 1 (`I`) less of 10 (`X`)
>
>Note: 49 is not 1 (`I`) less of 50 (`L`) because the conversion is based on decimal places

2. Case 2:
>Input: num = 58
>
>Output: `"LVIII"`
>
>Explanation:
>
>50 = `L`
>
> 8 = `VIII`

3. Case 3:
>Input: num = 1994
>
>Output: `"MCMXCIV"`
>
>Explanation:
>
>1000 = `M`
>
> 900 = `CM`
>
>  90 = `XC`
>
>   4 = `IV`

### Constraints
`1 < = num < = 3999`

---
## Python Solution
```python
def intToRoman(num):
    # Define the Roman numeral values and their corresponding integers
    value_symbols = [
        (1000, "M"), (900, "CM"), (500, "D"), (400, "CD"),
        (100, "C"), (90, "XC"), (50, "L"), (40, "XL"),
        (10, "X"), (9, "IX"), (5, "V"), (4, "IV"), (1, "I")
    ]
    
    # Initialize an empty string to store the Roman numeral result
    roman = ""
    
    # Iterate through the values and symbols
    for value, symbol in value_symbols:
        # Append the Roman numeral symbol for as many times as it fits in the number
        while num >= value:
            roman += symbol
            num -= value  # Reduce the number by the value of the Roman numeral

    return roman
```
---

### Explanation of the Solution
1. **Define Roman Numeral Mapping**:
   - A list of tuples is used to map integers to their corresponding Roman numeral symbols. The list is ordered from largest to smallest values to ensure the conversion starts with the highest value.
2. **Initialize Result String**:
   - Start with an empty string `roman` to accumulate the Roman numeral symbols.
3. **Iterate Through Values**:
   - Loop through the `value_symbols` list.
   - For each tuple `(value, symbol)`, check if the current number (`num`) is greater than or equal to the `value`.
   - Append the Roman numeral symbol (`symbol`) to the result as many times as the `value` fits into the number.
   - Subtract the `value` from the number each time the symbol is appended.
4. **Return the Result**:
   - After processing all the values, return the Roman numeral string.

### Example Walkthrough
**Input:** num = 2025

**Step 1: Process `1000 ("M")`**  
- `2025 >= 1000`: Yes. Append `"M"`, subtract 1000.  
  `roman = "M"`, `num = 1025`.
- `1025 >= 1000`: Yes. Append `"M"`, subtract 1000.  
  `roman = "MM"`, `num = 25`.
**Step 2: Process `10 ("X")`**  
- `25 >= 10`: Yes. Append `"X"`, subtract 10.  
  `roman = "MMX"`, `num = 15`.
- `15 >= 10`: Yes. Append `"X"`, subtract 10.  
  `roman = "MMXX"`, `num = 5`.
**Step 3: Process `5 ("V")`**  
- `5 >= 5`: Yes. Append `"V"`, subtract 5.  
  `roman = "MMXXV"`, `num = 0`.

**Output**: `"MMXXV"`
