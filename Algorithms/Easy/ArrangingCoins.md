![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 441. [Arranging Coins](https://leetcode.com/problems/arranging-coins)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def arrangeCoins(self, n: int) -> int:
        left = 1
        right = n
        while left <= right:
            middle = left + (right - left) // 2
            if middle*(middle+1) / 2 <= n:
                left = middle + 1
            else:
                right = middle - 1
        return right
```
