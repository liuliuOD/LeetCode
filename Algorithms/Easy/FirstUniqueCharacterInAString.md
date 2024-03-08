![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 387. [First Unique Character In A String](https://leetcode.com/problems/first-unique-character-in-a-string)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        counter = Counter(s)
        for index, char in enumerate(s):
            if counter[char] < 2:
                return index

        return -1
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        counter = [0] * 26
        for char in s:
            counter[self.getIndex(char)] += 1
        for index, char in enumerate(s):
            if counter[self.getIndex(char)] < 2:
                return index

        return -1

    def getIndex(self, char: str) -> int:
        return ord(char) - ord('a')
```
