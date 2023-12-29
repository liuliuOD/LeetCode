![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
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
