![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 342. [Power Of Four](https://leetcode.com/problems/power-of-four)

### Follow up:

- Could you solve it without loops/recursion?

### Solution :

Method 1 :
```python
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        # Option 1
        while n > 0 and n % 4 == 0:
            n //= 4
        """
        # Option 2

        if n <= 0:
            return False

        while n % 4 == 0:
            n //= 4
        """

        return n == 1
```

Method 2 :
```python
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        temp = 1
        while 0 < temp < n:
            temp *= 4

        return n == temp
```

Method 3 (Mathematic) :
```python
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        # n & (n-1) == 0 means n is power of 2
        if n <= 0 or (n & (n-1)) != 0:
            return False

        amount_zero = 0
        while (n & 1) == 0:
            amount_zero += 1
            n >>= 1

        return amount_zero % 2 == 0
```

Method 4 (Mathematic):
```python
class Solution:
    def isPowerOfFour(self, n: int) -> bool:
        # in hexidacimal, each 5 number means `0101` its the elementaries of power of 4
        mask = 0x55555555

        return n >= 1 and (n & (n-1)) == 0 and (n | mask) == mask
```
