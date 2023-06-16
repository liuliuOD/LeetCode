![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1569. [Number Of Ways To Reorder Array To Get Same BST](https://leetcode.com/problems/number-of-ways-to-reorder-array-to-get-same-bst)

### Solution :

Method 1 :
```python
import math
MOD = 10**9 + 7
class Solution:
    def numOfWays(self, nums: List[int]) -> int:
        return (self.dfs(nums) - 1) % MOD

    def combination(self, n: int, r: int) -> int:
        return math.factorial(n) // (math.factorial(r) * math.factorial(n - r))

    def dfs(self, nums: List[int]) -> int:
        if len(nums) <= 2:
            return 1
        left = list()
        right = list()
        for n in nums:
            if n == nums[0]:
                continue
            elif n < nums[0]:
                left.append(n)
            elif n > nums[0]:
                right.append(n)
        return self.combination(len(nums) - 1, len(left)) * self.dfs(left) * self.dfs(right)
```
