![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2919. [Minimum Increment Operations To Make Array Beautiful](https://leetcode.com/problems/minimum-increment-operations-to-make-array-beautiful)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def minIncrementOperations(self, nums: List[int], k: int) -> int:
        memoization = [-1] * len(nums)
        return self.dfs(0, memoization, k, nums)

    def dfs(self, index: int, memoization: List[int], k: int, nums: List[int]) -> int:
        n = len(nums)
        if index < n and memoization[index] >= 0:
            return memoization[index]

        if index > n-3:
            return 0

        memoization[index] = min(
            max(0, k-nums[index]) + self.dfs(index+1, memoization, k, nums),
            max(0, k-nums[index+1]) + self.dfs(index+2, memoization, k, nums),
            max(0, k-nums[index+2]) + self.dfs(index+3, memoization, k, nums)
        )
        return memoization[index]
```

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minIncrementOperations(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [-1] * n
        dp[0], dp[1], dp[2] = max(0, k-nums[0]), max(0, k-nums[1]), max(0, k-nums[2])
        for index in range(3, n):
            dp[index] = max(0, k-nums[index]) + min(dp[index-1], dp[index-2], dp[index-3])

        return min(dp[-1], dp[-2], dp[-3])
```

Method 3 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minIncrementOperations(self, nums: List[int], k: int) -> int:
        n = len(nums)
        # Option 1
        dp = deque([max(0, k-nums[0]), max(0, k-nums[1]), max(0, k-nums[2])])
        for index in range(3, n):
            dp.append(max(0, k-nums[index]) + min(dp[0], dp[1], dp[2]))
            dp.popleft()
        """
        # Option 2

        dp = [max(0, k-nums[0]), max(0, k-nums[1]), max(0, k-nums[2])]
        for index in range(3, n):
            dp[0], dp[1], dp[2] = dp[1], dp[2], max(0, k-nums[index]) + min(dp[0], dp[1], dp[2])
        """

        return min(dp)
```
