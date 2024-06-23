![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3196. [Maximize Total Cost Of Alternating Subarrays](https://leetcode.com/problems/maximize-total-cost-of-alternating-subarrays)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumTotalCost(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [[-inf, -inf] for _ in range(n)]
        dp[0][0] = dp[0][1] = nums[0]
        for index in range(1, n):
            dp[index][0] = nums[index] + max(dp[index-1][:])
            dp[index][1] = -nums[index] + dp[index-1][0]

        return max(dp[-1])
```

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maximumTotalCost(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [nums[0], nums[0]]
        for index in range(1, n):
            temp = [None, None]
            temp[0] = nums[index] + max(dp)
            temp[1] = -nums[index] + dp[0]
            dp = temp

        return max(dp)
```

Method 3 (Dynamic Programming + Space Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maximumTotalCost(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [nums[0], nums[0]]
        for index in range(1, n):
            dp = [nums[index] + max(dp), -nums[index] + dp[0]]

        return max(dp)
```
