![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2009. [Minimum Number Of Operations To Make Array Continuous](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-continuous)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def minOperations(self, nums: List[int]) -> int:
        n = len(nums)
        result = n
        nums = sorted(set(nums))
        n_set = len(nums)

        for index in range(n_set):
            # Find the maximum index of nums that <= current `num`+n-1
            left = 0
            right = n_set - 1
            maximum = nums[index] + n - 1
            while left <= right:
                index_search = left + (right - left)//2
                num = nums[index_search]
                if num <= maximum:
                    left = index_search + 1
                else:
                    right = index_search - 1

            result = min(result, n - (right-index+1))

        return result
```
