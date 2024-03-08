![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 377. [Combination Sum IV](https://leetcode.com/problems/combination-sum-iv)

### Solution :

Method 1 (Backtracking, Combination -> Permutation, ERROR: "Time Limit Exceeded", 14/15) :
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        nums.sort()
        combinations = []
        self.traverse(0, [], combinations, nums, target)

        result = 0
        for combination in combinations:
            counter = Counter(combination)
            result += reduce(lambda a, b: a*b, range(1, len(combination)+1)) // reduce(lambda a, b: a*b, [reduce(lambda a, b: a*b, range(1, value+1)) for value in counter.values()])

        return result

    def traverse(self, index: int, combination: List[int], combinations: List[List[int]], nums: List[int], target: int):
        amount = sum(combination)
        if amount > target or index >= len(nums):
            return

        if amount == target:
            combinations.append(combination)
            return

        self.traverse(index, combination + [nums[index]], combinations, nums, target)
        self.traverse(index+1, combination, combinations, nums, target)
```

Method 2 (DFS + Memoization) :
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        memoization = defaultdict(int)
        self.dfs(target, memoization, nums)

        return memoization[target]

    def dfs(self, target, memoization, nums) -> int:
        if target in memoization:
            return memoization[target]

        if target == 0:
            return 1

        if target < 0:
            return 0

        result = 0
        for num in nums:
            if target < num:
                continue

            result += self.dfs(target-num, memoization, nums)

        memoization[target] = result
        return result
```

Method 3 (Dynamic Programming) :
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        dp = [0] * (target+1)
        dp[0] = 1
        for index_dp in range(1, target+1):
            for num in nums:
                if index_dp-num < 0:
                    continue

                dp[index_dp] += dp[index_dp-num]

        return dp[target]
```
