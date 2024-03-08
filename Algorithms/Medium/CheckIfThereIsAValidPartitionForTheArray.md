![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2369. [Check If There Is A Valid Partition For The Array](https://leetcode.com/problems/check-if-there-is-a-valid-partition-for-the-array)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def validPartition(self, nums: List[int]) -> bool:
        if len(nums) <= 1:
            return False

        n = len(nums)
        memoization = [-1] * n
        return self.dfs(0, memoization, nums)

    def dfs(self, index: int, memoization: List[int], nums: List[int]) -> bool:
        n = len(nums)
        if index >= n:
            return True

        if memoization[index] != -1:
            return memoization[index]

        result = False
        index_next = index + 1
        # ex: [1, 1]
        if index_next < n and nums[index] == nums[index_next]:
            result |= self.dfs(index_next+1, memoization, nums)

        index_next_2 = index + 2
        # ex: [1, 1, 1]
        if index_next_2 < n and nums[index] == nums[index_next] == nums[index_next_2]:
            result |= self.dfs(index_next_2+1, memoization, nums)

        # ex: [1, 2, 3]
        if index_next_2 < n and nums[index]+1 == nums[index_next] and nums[index_next]+1 == nums[index_next_2]:
            result |= self.dfs(index_next_2+1, memoization, nums)

        memoization[index] = result
        return result
```
