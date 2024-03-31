![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2444. [Count Subarrays With Fixed Bounds](https://leetcode.com/problems/count-subarrays-with-fixed-bounds)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def countSubarrays(self, nums: List[int], minK: int, maxK: int) -> int:
        index_min = index_max = -1
        index_start = 0
        result = 0
        for index, num in enumerate(nums):
            if num < minK or num > maxK:
                index_start = index + 1
                index_min = index_max = -1

            if num == minK:
                index_min = index
            if num == maxK:
                index_max = index

            if index_min > -1 and index_max > -1:
                result += min(index_min, index_max) - index_start + 1

        return result
```
