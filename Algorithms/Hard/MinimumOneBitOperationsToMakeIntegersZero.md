![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1611. [Minimum One Bit Operations To Make Integers Zero](https://leetcode.com/problems/minimum-one-bit-operations-to-make-integers-zero)

### Solution :

Method 1 :
```python
class Solution:
    def minimumOneBitOperations(self, n: int) -> int:
        mapping = [(1<<index)-1 for index in range(1, 33)]
        bits_one = [index for index in range(0, 32) if (1<<index) & n == (1<<index)]

        result = 0
        for index, bit in enumerate(reversed(bits_one)):
            if index % 2 == 0:
                result += mapping[bit]
            else:
                result -= mapping[bit]

        return result
```
