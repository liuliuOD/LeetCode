![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1915. [Number Of Wonderful Substrings](https://leetcode.com/problems/number-of-wonderful-substrings)

### Solution :

Method 1 (Hash Map + Bitwise, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
BASE: int = ord("a")

class Solution:
    def wonderfulSubstrings(self, word: str) -> int:
        n = len(word)
        frequency: dict[int, int] = defaultdict(int)
        frequency[0] = 1
        mask = 0
        result = 0
        for index, char in enumerate(word):
            current = 1 << (ord(char) - BASE)
            mask ^= current
            if mask in frequency:
                result += frequency[mask]
            frequency[mask] += 1

            for index_bit in range(10):
                mask_odd = mask ^ (1 << index_bit)
                if mask_odd in frequency:
                    result += frequency[mask_odd]

        return result
```
