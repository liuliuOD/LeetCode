![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 68. [Text Justification](https://leetcode.com/problems/text-justification)

### Solution :

Method 1 (Greedy) :
```python
class Solution:
    def fullJustify(self, words: List[str], max_width: int) -> List[str]:
        n = len(words)
        # 1. calculate width of each words
        width_words = [len(word) for word in words]

        # 2. assemble text at each line
        result = []
        pointer_left = pointer_right = 0
        while pointer_right < n:
            if sum(width_words[pointer_left:pointer_right+1]) + (pointer_right-pointer_left) > max_width:
                result.append(self.formatWords(words[pointer_left:pointer_right], width_words[pointer_left:pointer_right], max_width))

                pointer_left = pointer_right
                continue

            if pointer_right == n-1:
                result.append(self.formatWords(words[pointer_left:pointer_right+1], width_words[pointer_left:pointer_right+1], max_width, True))

            pointer_right += 1

        return result

    def formatWords(self, words: List[str], width_words: List[str], max_width: int, is_last: bool = False) -> str:
        # For the last line of text, it should be left-justified, and no extra space is inserted between words.
        if is_last:
            line = ' '.join(words)
            return line + ' ' * (max_width-len(line))

        # For the other lines, they are fully-justified.
        amount = len(words)
        width_origin = sum(width_words)
        width_remaining = max_width - width_origin
        amount_slot = amount - 1 if amount > 1 else 1
        amount_space_base = width_remaining // amount_slot
        amount_space_remaining = width_remaining % amount_slot
        spaces = [' '*(amount_space_base + (1 if index < amount_space_remaining else 0)) for index in range(amount_slot)]

        result = ''
        for index, word in enumerate(words):
            result += word + (spaces[index] if index < len(spaces) else '')

        return result
```
