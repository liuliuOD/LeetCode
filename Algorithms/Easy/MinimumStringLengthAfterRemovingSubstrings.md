![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2696. [Minimum String Length After Removing Substrings](https://leetcode.com/problems/minimum-string-length-after-removing-substrings)

### Solution :

Method 1 (In weekly contest 346) :
```python
class Solution:
    def minLength(self, s: str) -> int:
        return self.remove(s)
    def remove(self, s: str) -> int:
        s_new = re.sub(r'(AB|CD)', '', s)
        if len(s) == len(s_new):
            return len(s)
        return self.remove(s_new)
```
