![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 8. [String To Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
THRESHOLD = 2**31
class Solution:
    def myAtoi(self, s: str) -> int:
        negative = False
        result = 0
        for index, char in enumerate(s.strip()):
            if index == 0 and char == '-':
                negative = True
                continue

            if index == 0 and char == '+':
                continue

            if ord('0') > ord(char) or ord(char) > ord('9'):
                break

            result = result * 10 + int(char)

        if negative:
            if result > THRESHOLD:
                result = THRESHOLD
            result *= -1
        elif result >= THRESHOLD:
            result = THRESHOLD - 1

        return result
```
