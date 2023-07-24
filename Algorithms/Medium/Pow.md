![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 50. [Pow(x, n)](https://leetcode.com/problems/powx-n)

### Solution :

Method 1 (Build-In Function) :
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        return x**n
```

Method 2 (Recursive, ERROR: "RecursionError: maximum recursion depth exceeded in comparison") :
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1.0
        elif n < 0:
            return 1.0 / self.myPow(x, -n)
        elif n > 0:
            return x * self.myPow(x, n-1)
```

Method 3 (Recursive + Mathematic) :
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1.0
        elif n < 0:
            return 1.0 / self.myPow(x, -n)

        if n % 2 == 1:
            return x * self.myPow(x*x, (n-1)//2)
        elif n % 2 == 0:
            return self.myPow(x*x, n//2)
```

Method 4 (Iterative) :
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1.0

        if n < 0:
            n = -n
            x = 1.0 / x

        result = 1.0
        while n > 0:
            if n % 2 == 1:
                result *= x
                n -= 1

            x *= x
            n = n // 2

        return result
```
