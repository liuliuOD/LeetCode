![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1404. [Number Of Steps To Reduce A Number In Binary Representation To One](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numSteps(self, s: str) -> int:
        decimal = int(s, 2)
        result = 0
        while decimal > 1:
            if decimal % 2 == 0:
                decimal //= 2
            else:
                decimal += 1

            result += 1

        return result
```
