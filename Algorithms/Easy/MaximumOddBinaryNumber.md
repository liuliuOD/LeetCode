![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2864. [Maximum Odd Binary Number](https://leetcode.com/problems/maximum-odd-binary-number)

### Solution :

Method 1 :
```python
class Solution:
    def maximumOddBinaryNumber(self, s: str) -> str:
        amount_one = s.count('1')
        amount_zero = len(s) - amount_one

        return '1'*(amount_one-1) + '0'*amount_zero + '1'
```

Method 2 :
```python
class Solution:
    def maximumOddBinaryNumber(self, s: str) -> str:
        s = list(s)
        n = len(s)
        pointer_zero = 0
        for index in range(n):
            if s[index] == '0':
                continue

            s[index], s[pointer_zero] = s[pointer_zero], s[index]
            pointer_zero += 1

        s[pointer_zero-1], s[n-1] = s[n-1], s[pointer_zero-1]
        return ''.join(s)
```
