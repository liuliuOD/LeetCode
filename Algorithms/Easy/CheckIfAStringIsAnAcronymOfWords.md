![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2828. [Check If A String Is An Acronym Of Words](https://leetcode.com/problems/check-if-a-string-is-an-acronym-of-words)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def isAcronym(self, words: List[str], s: str) -> bool:
        result = ''
        for word in words:
            result += word[0]

        return result == s
```

Method 2 (Pruning) :
```python
class Solution:
    def isAcronym(self, words: List[str], s: str) -> bool:
        n = len(s)
        if len(words) != n:
            return False

        for index, word in enumerate(words):
            if word[0] != s[index]:
                return False

        return True
```
