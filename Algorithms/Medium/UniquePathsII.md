![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 63. [Unique Paths II](https://leetcode.com/problems/unique-paths-ii)

### Solution :

Method 1 (Dynamic Programming, 1D) :
```rust
impl Solution {
    pub fn unique_paths_with_obstacles(obstacle_grid: Vec<Vec<i32>>) -> i32 {
        let m: usize = obstacle_grid.len();
        let n: usize = obstacle_grid[0].len();
        let mut dp: Vec<i32> = vec![0; n];
        dp[n-1] = match obstacle_grid[m-1][n-1] {
            0 => 1,
            _ => 0,
        };
        
        for index_m in (0..m).rev() {
            for index_n in (0..n).rev() {
                if obstacle_grid[index_m][index_n] == 1 {
                    dp[index_n] = 0;
                    continue;
                }

                if index_n+1 < n {
                    dp[index_n] += dp[index_n+1];
                }
            }
        }

        return dp[0]
    }
}
```

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacle_grid: List[List[int]]) -> int:
        self.m = len(obstacle_grid)
        self.n = len(obstacle_grid[0])
        memoization = [[-1]*self.n for _ in range(self.m)]
        return self.dfs(0, 0, memoization, obstacle_grid)

    def dfs(self, x: int, y: int, memoization: List[List[int]], obstacle_grid: List[List[int]]) -> int:
        if x >= self.m or y >= self.n or obstacle_grid[x][y] == 1:
            return 0

        if x == (self.m-1) and y == (self.n-1):
            return 1

        if memoization[x][y] != -1:
            return memoization[x][y]

        memoization[x][y] = self.dfs(x+1, y, memoization, obstacle_grid) + self.dfs(x, y+1, memoization, obstacle_grid)

        return memoization[x][y]
```

Method 2 (Dynamic Programming, 2D) :
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacle_grid: List[List[int]]) -> int:
        m = len(obstacle_grid)
        n = len(obstacle_grid[0])
        dp = [[0]*n for _ in range(m)]
        dp[-1][-1] = 1 if obstacle_grid[-1][-1] == 0 else 0
        for index_m in reversed(range(m)):
            for index_n in reversed(range(n)):
                if obstacle_grid[index_m][index_n] == 1:
                    continue

                if index_m+1 < m and obstacle_grid[index_m+1][index_n] != 1:
                    dp[index_m][index_n] += dp[index_m+1][index_n]

                if index_n+1 < n and obstacle_grid[index_m][index_n+1] != 1:
                    dp[index_m][index_n] += dp[index_m][index_n+1]
        return dp[0][0]
```

Method 3 (Dynamic Programming, 1D) :
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacle_grid: List[List[int]]) -> int:
        m = len(obstacle_grid)
        n = len(obstacle_grid[0])
        dp = [0] * n
        dp[-1] = 1 if obstacle_grid[-1][-1] == 0 else 0
        for index_m in reversed(range(m)):
            for index_n in reversed(range(n)):
                if obstacle_grid[index_m][index_n] == 1:
                    dp[index_n] = 0
                    continue

                if index_n+1 < n and obstacle_grid[index_m][index_n+1] != 1:
                    dp[index_n] += dp[index_n+1]

        return dp[0]
```
