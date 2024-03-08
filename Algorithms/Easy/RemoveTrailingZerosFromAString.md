![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2710. [Remove Trailing Zeros From A String](https://leetcode.com/problems/remove-trailing-zeros-from-a-string)

### Solution :

Method 1 (In weekly contest 347, regular expression) :
```python
class Solution:
    def removeTrailingZeros(self, num: str) -> str:
        result = re.sub('0*$', '', num)
        
        return result
```
