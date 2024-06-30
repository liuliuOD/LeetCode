![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3202. [Find The Maximum Length Of Valid Subsequence II](https://leetcode.com/problems/find-the-maximum-length-of-valid-subsequence-ii)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 709/732) :
```python
import copy

class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [defaultdict(lambda: 1) for _ in range(k)]
        for index, num in enumerate(nums):
            temp = copy.deepcopy(dp)
            for index_previous in range(index):
                num_previous = nums[index_previous]
                remainder = (num + num_previous) % k
                temp[remainder][num] = max(temp[remainder][num], dp[remainder][num_previous] + 1)

            dp = temp

        return max(max(group.values()) if group.values() else 0 for group in dp)
```

Method 2 (Hash Map, Time Complexity: $O(N^2)$, Space Complexity: $O(N*K)$) :
```python
class Solution:
    def maximumLength(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [defaultdict(lambda: 1) for _ in range(n)]
        for index, num in enumerate(nums):
            for index_previous in range(index):
                previous = nums[index_previous]
                remainder = (num + previous) % k
                dp[index][remainder] = max(dp[index][remainder], dp[index_previous][remainder] + 1)

        return max(max(group.values()) for group in dp)
```
