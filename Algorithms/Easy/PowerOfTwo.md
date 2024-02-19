![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 231. [Power Of Two](https://leetcode.com/problems/power-of-two)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        if n == 1:
            return True

        while n % 2 == 0 and n >= 2:
            n //= 2

        return n == 1
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        if n == 1:
            return True
        elif n == 0:
            return False

        while n % 2 == 0:
            n //= 2

        return n == 1
```

Method 3 (Bitwise, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        if n == 0:
            return False

        return n & (n-1) == 0
```
