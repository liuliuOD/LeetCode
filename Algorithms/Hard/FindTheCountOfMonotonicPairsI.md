![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3250. [Find The Count Of Monotonic Pairs I](https://leetcode.com/problems/find-the-count-of-monotonic-pairs-i)

### Solution :

Method 1 (DFS + Memoization) :
```python
MOD = 1_000_000_007
class Solution:
    def countOfPairs(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 1:
            return nums[0] + 1

        maximum = max(nums)
        memoization = [[-1] * (maximum+1) for _ in range(n)]
        return self.traverse(0, nums[0], 0, memoization, nums)

    def traverse(self, num_1_previous: int, num_2_previous: int, index: int, memoization: list[list[int]], nums: list[int]) -> int:
        if index >= len(nums):
            return 1

        if memoization[index][num_1_previous] >= 0:
            return memoization[index][num_1_previous]

        result = 0
        for num_1 in reversed(range(num_1_previous, nums[index]+1)):
            num_2 = nums[index] - num_1
            if num_2_previous < num_2:
                break

            result = (result + self.traverse(num_1, num_2, index+1, memoization, nums)) % MOD

        memoization[index][num_1_previous] = result
        return memoization[index][num_1_previous]
```
