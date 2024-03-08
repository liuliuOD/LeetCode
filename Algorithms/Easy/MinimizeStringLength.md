![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2716. [Minimize String Length](https://leetcode.com/problems/minimize-string-length)

### Solution :

Method 1 (In weekly contest 348) :
```python
class Solution:
    def minimizedStringLength(self, s: str) -> int:
        result = set()
        for c in s:
            result.add(c)
        
        return len(result)
```
