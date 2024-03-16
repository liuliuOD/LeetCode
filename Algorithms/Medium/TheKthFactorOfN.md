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
