![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 278. [First Bad Version](https://leetcode.com/problems/first-bad-version)

### Solution :

```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:
```

Method 1 (Binary Search) :
```python
class Solution:
    def firstBadVersion(self, n: int) -> int:
        left = 1
        right = n
        while left <= right:
            middle = left + (right - left) // 2
            if isBadVersion(middle):
                right = middle - 1
            else:
                left = middle + 1
        return left
```
