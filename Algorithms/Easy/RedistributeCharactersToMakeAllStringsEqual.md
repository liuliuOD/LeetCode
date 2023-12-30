![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1897. [Redistribute Characters To Make All Strings Equal](https://leetcode.com/problems/redistribute-characters-to-make-all-strings-equal)

### Solution :

Method 1 (Hash Map) :
```python
class Solution:
    def makeEqual(self, words: List[str]) -> bool:
        n = len(words)
        mapping = defaultdict(int)
        for word in words:
            for char in word:
                mapping[char] += 1

        return all([amount % n == 0 for amount in mapping.values()])
```

Method 2 (Array) :
```python
BASE = ord('a')
class Solution:
    def makeEqual(self, words: List[str]) -> bool:
        n = len(words)
        mapping = [0] * 26
        for word in words:
            for char in word:
                mapping[ord(char)-BASE] += 1

        return all([amount % n == 0 for amount in mapping])
```
