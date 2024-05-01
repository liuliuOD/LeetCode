![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2000. [Reverse Prefix Of Word](https://leetcode.com/problems/reverse-prefix-of-word)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def reversePrefix(self, word: str, ch: str) -> str:
        word = list(word)
        for index, char in enumerate(word):
            if char != ch:
                continue

            index_left = 0
            while index_left < index:
                word[index_left], word[index] = word[index], word[index_left]
                index_left += 1
                index -= 1
            break

        return ''.join(word)
```
