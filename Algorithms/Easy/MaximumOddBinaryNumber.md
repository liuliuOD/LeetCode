![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
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
