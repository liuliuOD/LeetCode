![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2971. [Find Polygon With The Largest Perimeter](https://leetcode.com/problems/find-polygon-with-the-largest-perimeter)

### Solution :

Method 1 (Sorting, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def largestPerimeter(self, nums: List[int]) -> int:
        result = 0
        perimeter = 0
        for num in sorted(nums):
            if perimeter > num:
                result = perimeter + num

            perimeter += num

        return result if result > 0 else -1
```
