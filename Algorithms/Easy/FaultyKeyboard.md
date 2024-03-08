![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2810. [Faulty Keyboard](https://leetcode.com/problems/faulty-keyboard)

### Solution :

Method 1 (In weekly contest 357) :
```python
class Solution:
    def finalString(self, s: str) -> str:
        result = []
        for char in s:
            if char == 'i':
                result.reverse()
                continue

            result.append(char)

        return ''.join(result)
```
