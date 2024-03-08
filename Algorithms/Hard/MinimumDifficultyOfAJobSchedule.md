![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1335. [Minimum Difficulty Of A Job Schedule](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule)

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def minDifficulty(self, job_difficulty: List[int], d: int) -> int:
        n = len(job_difficulty)
        if n < d:
            return -1

        memoization = defaultdict(int)
        return self.dfs(0, d, memoization, job_difficulty)

    def dfs(self, index: int, d: int, memoization: Dict[Tuple[int, int], int], job_difficulty: List[int]) -> int:
        n = len(job_difficulty)
        if d == 0:
            if index >= n:
                return 0
            else:
                return inf

        if index >= n:
            return inf

        key = (index, d)
        if key in memoization:
            return memoization[key]

        result = inf
        for index_next in range(index+1, n+1):
            result = min(result, max(job_difficulty[index:index_next])+self.dfs(index_next, d-1, memoization, job_difficulty))

        memoization[key] = result
        return result
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def minDifficulty(self, job_difficulty: List[int], d: int) -> int:
        n = len(job_difficulty)
        if n < d:
            return -1

        dp = [[inf]*(n+1) for _ in range(d+1)]
        dp[1][1] = job_difficulty[0]
        for index in range(2, n+1):
            dp[1][index] = max(dp[1][index-1], job_difficulty[index-1])

        for day in range(2, d+1):
            for index in range(day, n+1):
                maximum_remaining = job_difficulty[index-1]
                for index_previous in reversed(range(day, index+1)):
                    maximum_remaining = max(maximum_remaining, job_difficulty[index_previous-1])
                    dp[day][index] = min(dp[day][index], dp[day-1][index_previous-1] + maximum_remaining)

        return -1 if dp[d][n] is inf else dp[d][n]
```

Method 3 (Dynamic Programming + Space Optimization) :
```python
class Solution:
    def minDifficulty(self, job_difficulty: List[int], d: int) -> int:
        n = len(job_difficulty)
        if n < d:
            return -1

        dp = [inf] * (n+1)
        dp[1] = job_difficulty[0]
        for index in range(2, n+1):
            dp[index] = max(dp[index-1], job_difficulty[index-1])

        for day in range(2, d+1):
            temp = [inf] * (n+1)
            for index in range(day, n+1):
                maximum_remaining = job_difficulty[index-1]
                for index_previous in reversed(range(day, index+1)):
                    maximum_remaining = max(maximum_remaining, job_difficulty[index_previous-1])
                    temp[index] = min(temp[index], dp[index_previous-1] + maximum_remaining)

            dp = temp

        return -1 if dp[n] is inf else dp[n]
```
