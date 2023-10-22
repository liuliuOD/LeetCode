![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2909. [Minimum Sum Of Mountain Triplets II](https://leetcode.com/problems/minimum-sum-of-mountain-triplets-ii)

### Solution :

Method 1 (In weekly contest 368, Prefix Sum + Suffix Sum) :
```python
class Solution:
    def minimumSum(self, nums: List[int]) -> int:
        n = len(nums)

        # Prefix Sum
        minimum_left = [None] * n
        for index in range(n):
            if index > 0 and (nums[index-1] < nums[index] or (minimum_left[index-1] and minimum_left[index-1] < nums[index])):
                minimum_left[index] = min(nums[index-1], minimum_left[index-1] if minimum_left[index-1] else inf)

        # Suffix Sum
        minimum_right = [None] * n
        for index in reversed(range(n)):
            if index+1 < n and (nums[index+1] < nums[index] or (minimum_right[index+1] and minimum_right[index+1] < nums[index])):
                minimum_right[index] = min(nums[index+1], minimum_right[index+1] if minimum_right[index+1] else inf)

        result = inf
        for index in range(1, n-1):
            if minimum_left[index] is None or minimum_right[index] is None:
                continue

            result = min(result, minimum_left[index]+minimum_right[index]+nums[index])

        return -1 if result == inf else result
```

Method 2 (Prefix Sum + Suffix Sum) :
```python
class Solution:
    def minimumSum(self, nums: List[int]) -> int:
        n = len(nums)
        minimum_left = [inf] * n
        for index in range(n):
            if index-1 >= 0 and (nums[index-1] < nums[index] or minimum_left[index-1] < nums[index]):
                minimum_left[index] = min(nums[index-1], minimum_left[index-1])

        minimum_right = [inf] * n
        for index in reversed(range(n)):
            if index+1 < n and (nums[index+1] < nums[index] or minimum_right[index+1] < nums[index]):
                minimum_right[index] = min(nums[index+1], minimum_right[index+1])

        result = inf
        for index in range(1, n-1):
            if minimum_left[index] is inf or minimum_right[index] is inf:
                continue

            result = min(result, minimum_left[index]+minimum_right[index]+nums[index])

        return -1 if result == inf else result
```
