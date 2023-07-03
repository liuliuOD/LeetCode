![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1025. [Divisor Game](https://leetcode.com/problems/divisor-game)

### Solution :

Method 1 (Recursive) :
```python
class Solution:
    def divisorGame(self, n: int) -> bool:
        return self.move(n)

    def move(self, n: int) -> bool:
        if n == 1:
            return False
        elif n == 2:
            return True

        return self.move(n-1)^1
```

Method 2 ([Reference](https://leetcode.com/problems/divisor-game/solutions/296784/come-on-in-different-explanation-from-others/)) :
```python
class Solution:
    def divisorGame(self, n: int) -> bool:
        return n % 2 == 0
```
