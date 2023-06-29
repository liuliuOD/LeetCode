![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 746. [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs)

### Solution :

Method 1 (Recursive, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        self.cost = cost
        return min(self.dfs(0, 0), self.dfs(1, 0))

    def dfs(self, index: int, total_cost: int) -> int:
        if index >= len(self.cost):
            return total_cost
        
        total_cost += self.cost[index]
        return min(self.dfs(index+1, total_cost), self.dfs(index+2, total_cost))
```

Method 2 (Bottom Up, Dynamic Programming + Memoization, Space Complexity: O(N)) :
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        n = len(cost)
        memoization = defaultdict(lambda: float('inf'))
        memoization[0], memoization[1] = cost[0], cost[1]
        for index in range(2, n):
            memoization[index] = cost[index] + min(memoization[index-1], memoization[index-2])
        
        return min(memoization[n-1], memoization[n-2])
```

Method 3 (Bottom Up, Dynamic Programming + Memoization, Space Complexity: O(1)) :
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        n = len(cost)
        memoization_1_step = cost[0]
        memoization_2_step = cost[1]

        for index in range(2, n):
            temp = cost[index] + min(memoization_1_step, memoization_2_step)
            memoization_1_step = memoization_2_step
            memoization_2_step = temp
        
        return min(memoization_1_step, memoization_2_step)
```

Method 4 (Top Down, Dynamic Programming + Memoization) :
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        self.cost = cost
        self.memoization = {}
        return min(self.dfs(len(cost)-1), self.dfs(len(cost)-2))
    
    def dfs(self, index: int) -> int:
        if index in [0, 1]:
            return self.cost[index]
        
        if index in self.memoization:
            return self.memoization[index]
        
        self.memoization[index] = self.cost[index] + min(self.dfs(index-1), self.dfs(index-2))
        return self.memoization[index]
```

Method 5 (Top Down, Dynamic Programming + Memoization, set Base Case to Memoization) :
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        self.cost = cost
        self.memoization = {0: cost[0], 1: cost[1]}
        return min(self.dfs(len(cost)-1), self.dfs(len(cost)-2))
    
    def dfs(self, index: int) -> int:
        if index in self.memoization:
            return self.memoization[index]
        
        self.memoization[index] = self.cost[index] + min(self.dfs(index-1), self.dfs(index-2))
        return self.memoization[index]
```

Method 6 (Bottom Up, Dynamic Programming + Memoization) :
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        self.cost = cost
        self.memoization = {}
        return min(self.dfs(0), self.dfs(1))

    def dfs(self, index: int) -> int:
        if index >= len(self.cost):
            return 0
        
        if index in self.memoization:
            return self.memoization[index]
        
        self.memoization[index] = self.cost[index] + min(self.dfs(index+1), self.dfs(index+2))
        return self.memoization[index]
```
