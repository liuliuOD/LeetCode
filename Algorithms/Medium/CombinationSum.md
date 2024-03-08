![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 39. [Combination Sum](https://leetcode.com/problems/combination-sum)

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        self.result = []
        self.dfs(0, target, [], candidates)
        return self.result

    def dfs(self, index, target, group, candidates):
        if target <= 0 or index >= len(candidates):
            if target == 0:
                self.result.append(group)
            return None

        targetCurrent = candidates[index]
        self.dfs(index, target-targetCurrent, group + [targetCurrent], candidates)
        self.dfs(index+1, target, group, candidates)
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        n = len(candidates)
        dp = [[] for _ in range(target+1)]
        for candidate in candidates:
            if candidate <= target:
                dp[candidate].append([candidate])

            for targetCurrent in range(candidate+1, target+1):
                for combination in dp[targetCurrent-candidate]:
                    dp[targetCurrent].append(combination+[candidate])

        return dp[-1]
```
