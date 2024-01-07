![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 446. [Arithmetic Slices II - Subsequence](https://leetcode.com/problems/arithmetic-slices-ii-subsequence)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def numberOfArithmeticSlices(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 3:
            return 0

        mapping = defaultdict(list)
        for index in range(n):
            mapping[nums[index]].append(index)

        memoization = defaultdict(int)
        result = 0
        for index_first in range(n):
            for index_second in range(index_first+1, n):
                result += self.dfs(2, index_second, nums[index_second]-nums[index_first], memoization, mapping, nums)

        return result

    def dfs(self, amount, index, difference, memoization, mapping, nums) -> int:
        n = len(nums)
        if index >= n:
            return 0

        key = (index, difference, amount)
        if key in memoization:
            return memoization[key]

        result = 0 if amount < 3 else 1
        num_next = nums[index] + difference
        # Option 1
        if num_next in mapping:
            for index_next in mapping[num_next]:
                if index >= index_next:
                    continue

                result += self.dfs(amount+1, index_next, difference, memoization, mapping, nums)
        """
        # Option 2

        if num_next not in mapping:
            return result

        for index_next in mapping[num_next]:
            if index >= index_next:
                continue

            result += self.dfs(amount+1, index_next, difference, memoization, mapping, nums)
        """

        memoization[key] = result
        return result
```
