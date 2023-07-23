![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2788. [Split Strings By Separator](https://leetcode.com/problems/split-strings-by-separator)

### Solution :

Method 1 :
```python
class Solution:
    def splitWordsBySeparator(self, words: List[str], separator: str) -> List[str]:
        result = []
        for word in words:
            for item in word.split(separator):
                if item != '':
                    result.append(item)
        return result
```
