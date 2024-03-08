![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2744. [Find Maximum Number Of String Pairs](https://leetcode.com/problems/find-maximum-number-of-string-pairs)

### Solution :

Method 1 (In biweekly contest 107) :
```python
class Solution:
    def maximumNumberOfStringPairs(self, words: List[str]) -> int:
        n = len(words)
        result = 0
        for i in range(n):
            for j in range(i+1, n):
                if words[i] == words[j][::-1]:
                    result += 1
                    break
        return result
```
