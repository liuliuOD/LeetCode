![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 3122. [Minimum Number Of Operations To Satisfy Conditions](https://leetcode.com/problems/minimum-number-of-operations-to-satisfy-conditions)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def minimumOperations(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        counter = [[0] * 10 for _ in range(n)]
        for index_n in range(n):
            for index_m in range(m):
                counter[index_n][grid[index_m][index_n]] += 1

        memoization = [[-1]*10 for _ in range(n)]
        return m*n - self.dfs(0, 0, memoization, counter)

    def dfs(self, index_n: int, column_value: int, memoization, counter) -> int:
        # len(counter) == n
        if index_n >= len(counter):
            return 0

        if memoization[index_n][column_value] == -1:
            for column_value_next in range(10):
                if index_n != 0 and column_value == column_value_next:
                    continue

                memoization[index_n][column_value] = max(memoization[index_n][column_value], counter[index_n][column_value_next] + self.dfs(index_n+1, column_value_next, memoization, counter))

        return memoization[index_n][column_value]
```

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```go
func minimumOperations(grid [][]int) int {
    m, n := len(grid), len(grid[0])
    counter := make([][10]int, n)
    for index_n := 0; index_n < n; index_n++ {
        for index_m := 0; index_m < m; index_m++ {
            counter[index_n][grid[index_m][index_n]] += 1
        }
    }

    memoization := make([][10]int, n)
    return m*n - dfs(0, 0, &memoization, &counter)
}

func dfs(index_n, value_previous int, memoization, counter *[][10]int) int {
    if index_n >= len(*counter) {
        return 0
    }

    if (*memoization)[index_n][value_previous] == 0 {
        for value_next := 0; value_next <= 9; value_next++ {
            if index_n != 0 && value_previous == value_next {
                continue
            }

            (*memoization)[index_n][value_previous] = max((*memoization)[index_n][value_previous], (*counter)[index_n][value_next] + dfs(index_n+1, value_next, memoization, counter))
        }
    }
    return (*memoization)[index_n][value_previous]
}
```
