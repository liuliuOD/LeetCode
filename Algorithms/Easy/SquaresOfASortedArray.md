![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 977. [Squares Of A Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array)

### Solution :

Method 1 :
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        return sorted([num**2 for num in nums])
```
