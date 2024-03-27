![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 713. [Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        result = 0
        product = 1
        left = 0
        for right, num in enumerate(nums):
            product *= num
            while left <= right and product >= k:
                product /= nums[left]
                left += 1

            result += right - left + 1

        return result
```
