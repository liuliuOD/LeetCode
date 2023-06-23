![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1027. [Longest Arithmetic Subsequence](https://leetcode.com/problems/longest-arithmetic-subsequence)

### Solution :

Method 1 (Dynamic Programming) :
```python
class Solution:
    def longestArithSeqLength(self, nums: List[int]) -> int:
        dp = {}
        for i in range(len(nums)-1):
            for j in range(i+1, len(nums)):
                difference = nums[j] - nums[i]
                dp[j, difference] = dp.get((i, difference), 1) + 1
        return max(dp.values())
```
