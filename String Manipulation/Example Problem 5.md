# Example Problem 5: Text Justification

## Problem Statement
Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

Note:
- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than `0` and not exceed `maxWidth`.
- The input array `words` contains at least one word.

### Example Cases
1. Case 1:
>Input: words = `["This", "is", "an", "example", "of", "text", "justification."]`, maxWidth = 16
>
>Output:
>```
>[
>   "This    is    an",
>
>   "example  of text",
>
>   "justification.  "
>]
>```

2. Case 2:
>Input: words = `["What","must","be","acknowledgment","shall","be"]`, maxWidth = 16
>
>Output:
>
>```
>[
>  "What   must   be",
>
>  "acknowledgment  ",
>
>  "shall be        "
>]
>```
>Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.

### Constraints
`1 < = words.length < = 300`

`1 < = words[i].length < = 20`

`words[i]` consists of only English letters and symbols.

`1 < = maxWidth < = 100`

`words[i].length < = maxWidth`

---

## Python Solution
```python
def fullJustify(words, maxWidth):
    result = []
    current_line = []
    current_length = 0

    for word in words:
        # Check if adding this word exceeds maxWidth
        if current_length + len(word) + len(current_line) > maxWidth:
            # Distribute spaces for the current line
            for i in range(maxWidth - current_length):
                current_line[i % (len(current_line) - 1 or 1)] += ' '
            result.append(''.join(current_line))
            current_line = []
            current_length = 0

        # Add the word to the current line
        current_line.append(word)
        current_length += len(word)

    # Handle the last line (left-justified)
    result.append(' '.join(current_line).ljust(maxWidth))

    return result
```
---

### Explanation of the Solution

1. **Core Logic**:
   - Maintain a list `current_line` to store words that can fit in the current line.
   - Maintain `current_length` to track the total length of characters in the `current_line` (excluding spaces).
   - If adding a new word causes the line to exceed `maxWidth`, distribute spaces evenly across the words in `current_line` and add the line to the result.

2. **Space Distribution**:
   - Distribute spaces evenly among the words in `current_line` by iterating over the slots (using `i % (len(current_line) - 1)`).
   - If there is only one word in the line, all spaces are appended to the end of the word.

3. **Last Line Handling**:
   - For the last line, words are left-justified (spaces added at the end to reach `maxWidth`).

4. **Efficiency**:
   - The algorithm iterates through the words and adjusts spacing in \(O(n)\) time, where \(n\) is the total number of characters in `words`.

### Example Walkthrough

**Input:**
```python
words = ["This", "is", "an", "example", "of", "text", "justification."]
maxWidth = 16
```
1. **First Iteration**:
   - `current_line = ["This", "is", "an"]`
   - `current_length = 8` (`len("This") + len("is") + len("an")`)
   - Adding "example" exceeds `maxWidth = 16`, so:
     - Distribute spaces: `"This  is  an"`
     - Append to result: `["This  is  an"]`
   - Reset `current_line = ["example"]`, `current_length = 7`

2. **Second Iteration**:
   - Add "of" and "text" to `current_line`:
     - `current_line = ["example", "of", "text"]`
     - `current_length = 13`
   - Adding "justification." exceeds `maxWidth = 16`, so:
     - Distribute spaces: `"example of text"`
     - Append to result: `["This  is  an", "example of text"]`
   - Reset `current_line = ["justification."]`, `current_length = 14`

3. **Final Step**:
   - Handle the last line (left-justified):
     - `current_line = ["justification."]`
     - Append with padding: `"justification.  "`
   - Result becomes: `["This  is  an", "example of text", "justification.  "]`

**Output:**
```python
[
    "This  is  an",
    "example of text",
    "justification.  "
]
```
