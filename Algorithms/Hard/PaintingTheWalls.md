![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2742. [Painting The Walls](https://leetcode.com/problems/painting-the-walls)

### Solution :

Method 1 (DFS + Memoization, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def paintWalls(self, costs: List[int], times: List[int]) -> int:
        memoization = defaultdict(int)
        return self.dfs(set(), 0, 0, memoization, costs, times)

    def dfs(self, visited: Set[int], cost_sum: int, time_sum: int, memoization: Dict[str, int], costs: List[int], times: List[int]):
        key = '-'.join(map(str, sorted(list(visited))))
        if key in memoization:
            return memoization[key]

        n = len(costs)
        if len(visited) + time_sum >= n:
            return cost_sum

        result = inf
        for index in range(n):
            if index in visited:
                continue

            temp = visited.copy()
            temp.add(index)
            result = min(result, self.dfs(temp, cost_sum+costs[index], time_sum+times[index], memoization, costs, times))

        memoization[key] = result
        return result
```

Method 2 (DFS + Memoization, Time Complexity: $O(N^2)$ (N: length of parameter `costs`)) :
```python
class Solution:
    def paintWalls(self, costs: List[int], times: List[int]) -> int:
        memoization = defaultdict(int)
        return self.dfs(0, len(costs), memoization, costs, times)

    def dfs(self, index: int, amount_remaining: int, memoization: Dict[str, int], costs: List[int], times: List[int]):
        key = f'{index}-{amount_remaining}'
        if key in memoization:
            return memoization[key]

        if amount_remaining <= 0:
            return 0

        if index >= len(costs):
            return inf

        # Option 1
        memoization[key] = min(0 + self.dfs(index+1, amount_remaining, memoization, costs, times), costs[index] + self.dfs(index+1, amount_remaining - times[index] - 1, memoization, costs, times))
        """
        # Option 2

        non_choose = self.dfs(index+1, amount_remaining, memoization, costs, times)
        choose = costs[index] + self.dfs(index+1, amount_remaining - times[index] - 1, memoization, costs, times)
        memoization[key] = min(non_choose, choose)
        """

        return memoization[key]
```

Method 3 (Dynamic Programming, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def paintWalls(self, costs: List[int], times: List[int]) -> int:
        n = len(costs)
        dp = [[0]*(n+1) for _ in range(n+1)]
        for index in range(1, n+1):
            dp[n][index] = inf

        for index in reversed(range(n)):
            for amount_remaining in range(n+1):
                dp[index][amount_remaining] = min(dp[index+1][amount_remaining], costs[index] + dp[index+1][max(0, amount_remaining-times[index]-1)])

        return dp[0][n]
```

Method 4 (Dynamic Programming, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def paintWalls(self, costs: List[int], times: List[int]) -> int:
        n = len(costs)
        dp = [inf] * (n+1)
        dp[0] = 0
        for index in reversed(range(n)):
            temp_dp = [0] * (n+1)
            for amount_remaining in range(n+1):
                temp_dp[amount_remaining] = min(dp[amount_remaining], costs[index] + dp[max(0, amount_remaining-times[index]-1)])

            dp = temp_dp

        return dp[n]
```
