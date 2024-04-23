![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3117. [Minimum Sum Of Values By Dividing Array](https://leetcode.com/problems/minimum-sum-of-values-by-dividing-array)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def minimumValueSum(self, nums: List[int], and_values: List[int]) -> int:
        m = len(nums)
        n = len(and_values)
        memoization: Dict[str, int] = dict()
        result = self.dfs(0, 0, -1, memoization, nums, and_values)
        return -1 if result is inf else result

    def dfs(self, index_nums: int, index_and_values: int, bitwise: int, memoization: Dict[str, int], nums: List[int], and_values: List[int]) -> int:
        if index_nums >= len(nums) and index_and_values >= len(and_values):
            return 0
        elif index_nums >= len(nums) or index_and_values >= len(and_values):
            return inf

        key = f"{index_nums}-{index_and_values}-{bitwise}"
        if key in memoization:
            return memoization[key]

        bitwise_next = bitwise & nums[index_nums]
        result = self.dfs(index_nums+1, index_and_values, bitwise_next, memoization, nums, and_values)
        if bitwise_next == and_values[index_and_values]:
            result = min(result, nums[index_nums] + self.dfs(index_nums+1, index_and_values+1, -1, memoization, nums, and_values))

        memoization[key] = result
        return result
```

Method 2 (DFS + Built-In Cache, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def minimumValueSum(self, nums: List[int], and_values: List[int]) -> int:
        m = len(nums)
        n = len(and_values)

        @cache
        def dfs(index_nums: int, index_and_values: int, bitwise: int) -> int:
            if index_nums >= m and index_and_values >= n:
                return 0
            elif index_nums >= m or index_and_values >= n:
                return inf

            bitwise &= nums[index_nums]

            result = dfs(index_nums+1, index_and_values, bitwise)
            if bitwise == and_values[index_and_values]:
                result = min(result, nums[index_nums] + dfs(index_nums+1, index_and_values+1, -1))

            return result

        result = dfs(0, 0, -1)
        return -1 if result is inf else result
```
