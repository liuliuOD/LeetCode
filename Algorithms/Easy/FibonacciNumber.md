![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 509. [Fibonacci Number](https://leetcode.com/problems/fibonacci-number)

### Solution :

Method 1 (Recursive) :
```python
class Solution:
    def fib(self, n: int) -> int:
        if n <= 1:
            return n
        return self.fib(n-1) + self.fib(n-2)
```

Method 2 (Bottom Up, Dynamic Programming + Memoization) :
```python
class Solution:
    def fib(self, n: int) -> int:
        memoization = {0: 0, 1: 1}
        for index in range(2, n+1):
            memoization[index] = memoization[index-1] + memoization[index-2]
        return memoization[n]
```

Method 3 (Bottom Up, Dynamic Programming + Memoization, Space Complexity: O(1)) :
```python
class Solution:
    def fib(self, n: int) -> int:
        memoization_1 = 0
        memoization_2 = 1
        for index in range(2, n+1):
            temp = memoization_1 + memoization_2
            memoization_1 = memoization_2
            memoization_2 = temp
        return memoization_2 if n > 0 else memoization_1
```

Method 4 (Top Down, Dynamic Programming + Memoization) :
```python
class Solution:
    def fib(self, n: int) -> int:
        self.memoization = {0: 0, 1: 1}
        
        return self.dynamicProgramming(n)
    
    def dynamicProgramming(self, n: int) -> int:
        if n in self.memoization:
            return self.memoization[n]
        
        self.memoization[n] = self.dynamicProgramming(n-1) + self.dynamicProgramming(n-2)
        return self.memoization[n]
```
