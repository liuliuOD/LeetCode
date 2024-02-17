![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1642. [Furthest Building You Can Reach](https://leetcode.com/problems/furthest-building-you-can-reach)

### Solution :

Method 1 (DFS, ERROR: "Memory Limit Exceeded") :
```python
class Solution:
    def furthestBuilding(self, buildings: List[int], bricks: int, ladders: int) -> int:
        memoization = defaultdict(int)
        return self.dfs(1, bricks, ladders, memoization, buildings) - 1

    def dfs(self, index: int, bricks: int, ladders: int, memoization, buildings: List[int]) -> int:
        n = len(buildings)
        if index >= n:
            return index

        key = (index, bricks, ladders)
        if key in memoization:
            return memoization[key]

        result = index
        if buildings[index] <= buildings[index-1]:
            result = self.dfs(index+1, bricks, ladders, memoization, buildings)
        else:
            difference = buildings[index] - buildings[index-1]
            if bricks >= difference:
                result = max(result, self.dfs(index+1, bricks-difference, ladders, memoization, buildings))
            if ladders:
                result = max(result, self.dfs(index+1, bricks, ladders-1, memoization, buildings))

        memoization[key] = result
        return result
```
