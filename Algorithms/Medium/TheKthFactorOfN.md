![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1492. [The Kth Factor Of N](https://leetcode.com/problems/the-kth-factor-of-n)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def kthFactor(self, n: int, k: int) -> int:
        current = 0
        counter = 0
        while current < n:
            current += 1
            if n % current == 0:
                counter += 1
                if counter == k:
                    return current

        return -1
```

Method 2 (Time Complexity: $O(Sqrt(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def kthFactor(self, n: int, k: int) -> int:
        square_root = n**0.5
        factors_larger_than_root = []

        for i in range(1, int(square_root) + 1):
            if n % i != 0:
                continue

            k -= 1
            if k == 0:
                return i

            factors_larger_than_root.append(n // i)

        if int(square_root) == square_root:
            factors_larger_than_root.pop()

        if k <= len(factors_larger_than_root):
            return factors_larger_than_root[-k]

        return -1
```
