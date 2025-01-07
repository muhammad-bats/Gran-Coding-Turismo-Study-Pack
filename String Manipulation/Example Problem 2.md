# Example Problem 2: Find the Index of the First Occurrence in a String

## Problem Statement
Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

### Example Cases

1. Case 1:
>Input:
>haystack = "sadbutsad"
>
>    needle = "sad"
>
>Output:
>0
>
>Explanation: "sad" occurs at index 0 and 6. The first occurrence is at index 0, so we return 0.

2. Case 2:
>Input:
>haystack = "GranTurismo"
>
>    needle = "Tour"
>
>Output:
>-1
>
>Explanation: "Tour" did not occur in "GranTurismo", so we return -1.

### Constraints:
- `1 <= haystack.length, needle.length <= 10^3`
- `haystack` and `needle` consist of only lowercase English characters.

---

## Solution
The task is to find the index of the first occurrence of `needle` in `haystack`. If `needle` is not found, return `-1`. This can be achieved using Python’s built-in string methods or by implementing a custom solution.

Below is the Python solution with an explanation:

## Python Solution:
```python
def strStr(haystack: str, needle: str) -> int:
    # Edge case: If needle is an empty string, return -1
    if not needle:
        return -1

    # Use Python's built-in string find method
    index = haystack.find(needle)

    return index

# Example usage:
haystack1 = "beaconhouse"
needle1 = "con"
print(strStr(haystack1, needle1))  # Output: 3

haystack2 = "bna2025"
needle2 = "24"
print(strStr(haystack2, needle2))  # Output: -1
```

---

## Explanation of the Solution:
1. **Edge Case Handling:** If the `needle` is an empty string, the function directly returns `-1`, as per the problem definition.

2. **Finding the First Occurrence:** The `find` method of Python strings returns the index of the first occurrence of a substring. If the substring is not found, it returns `-1`. This method is efficient and simplifies the implementation.

3. **Return the Result:** The function returns the index of the first occurrence or `-1` if `needle` is not found.
