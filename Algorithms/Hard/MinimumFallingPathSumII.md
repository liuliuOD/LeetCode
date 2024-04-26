![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1289. [Minimum Falling Path Sum II](https://leetcode.com/problems/minimum-falling-path-sum-ii)

### Solution :

Method 1 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn min_falling_path_sum(grid: Vec<Vec<i32>>) -> i32 {
        let mut min_1: [Option<i32>; 2] = [Some(0), Some(0)];
        let mut min_2: [Option<i32>; 2] = [Some(0), Some(0)];
        for row in grid.into_iter() {
            let mut temp_min_1: [Option<i32>; 2] = [None, None];
            let mut temp_min_2: [Option<i32>; 2] = [None, None];
            for (index, mut current) in row.into_iter().enumerate() {
                let index: i32 = index as i32;
                if index == min_1[0].unwrap() {
                    current += min_2[1].unwrap();
                } else {
                    current += min_1[1].unwrap();
                }

                if temp_min_1[0].is_none() || temp_min_1[1].unwrap() > current {
                    temp_min_2 = temp_min_1;
                    temp_min_1 = [Some(index), Some(current)];
                } else if temp_min_2[0].is_none() || temp_min_2[1].unwrap() > current {
                    temp_min_2 = [Some(index), Some(current)];
                }
            }

            min_1 = temp_min_1;
            min_2 = temp_min_2;
        }

        return min_1[1].unwrap_or(0)
    }
}
```

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn min_falling_path_sum(grid: Vec<Vec<i32>>) -> i32 {
        let mut min_1: [i32; 2] = [0, 0];
        let mut min_2: [i32; 2] = [0, 0];
        for row in grid.into_iter() {
            let mut temp_min_1: [i32; 2] = [-1, -1];
            let mut temp_min_2: [i32; 2] = [-1, -1];
            for (index, mut current) in row.into_iter().enumerate() {
                let index: i32 = index as i32;
                if index == min_1[0] {
                    current += min_2[1];
                } else {
                    current += min_1[1];
                }

                if temp_min_1[0] == -1 || temp_min_1[1] > current {
                    temp_min_2 = temp_min_1;
                    temp_min_1 = [index, current];
                } else if temp_min_2[0] == -1 || temp_min_2[1] > current {
                    temp_min_2 = [index, current];
                }
            }

            min_1 = temp_min_1;
            min_2 = temp_min_2;
        }

        return min_1[1]
    }
}
```

### Solution :

Method 1 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^3)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minFallingPathSum(self, grid: List[List[int]]) -> int:
        n = len(grid)
        dp = [0] * n
        for row in grid:
            temp = [inf] * n
            for index, column in enumerate(row):
                temp[index] = column
                if len(row) > 1:
                    temp[index] += min(dp[:index] + dp[index+1:])
            dp = temp

        return min(dp)
```

Method 2 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minFallingPathSum(self, grid: List[List[int]]) -> int:
        n = len(grid)
        if n == 1:
            return grid[0][0]

        dp = [0] * n
        index_min_1, index_min_2 = 0, 0
        for row in grid:
            temp = [inf] * n
            temp_index_min_1, temp_index_min_2 = None, None
            for index, column in enumerate(row):
                temp[index] = column
                if index == index_min_1:
                    temp[index] += dp[index_min_2]
                elif index == index_min_2:
                    temp[index] += dp[index_min_1]
                else:
                    temp[index] += min(dp[index_min_1], dp[index_min_2])

                if temp_index_min_1 is None or temp[index] < temp[temp_index_min_1]:
                    temp_index_min_1, temp_index_min_2 = index, temp_index_min_1
                elif temp_index_min_2 is None or temp[index] < temp[temp_index_min_2]:
                    temp_index_min_2 = index

            dp = temp
            index_min_1, index_min_2 = temp_index_min_1, temp_index_min_2

        return min(dp)
```

Method 3 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minFallingPathSum(self, grid: List[List[int]]) -> int:
        n = len(grid)
        if n == 1:
            return grid[0][0]

        min_1, min_2 = (0, 0), (0, 0)
        for row in grid:
            temp_min_1, temp_min_2 = None, None
            for index, column in enumerate(row):
                current = column
                if index == min_1[1]:
                    current += min_2[0]
                elif index == min_2[1]:
                    current += min_1[0]
                else:
                    current += min(min_1[0], min_2[0])

                if temp_min_1 is None or current < temp_min_1[0]:
                    temp_min_1, temp_min_2 = (current, index), temp_min_1
                elif temp_min_2 is None or current < temp_min_2[0]:
                    temp_min_2 = (current, index)

            min_1, min_2 = temp_min_1, temp_min_2

        return min(min_1[0], min_2[0])
```

### Solution :

Method 1 (Dynamic Programming + Space Optimization, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```go
func minFallingPathSum(grid [][]int) int {
    min_1, min_2 := []int{0, 0}, []int{0, 0}
    for _, row := range grid {
        temp_min_1, temp_min_2 := []int{-100, 0}, []int{-100, 0}
        for index, current := range row {
            if index == min_1[0] {
                current += min_2[1]
            } else {
                current += min_1[1]
            }

            if temp_min_1[0] == -1 || temp_min_1[1] > current {
                temp_min_2 = temp_min_1
                temp_min_1 = []int{index, current}
            } else if temp_min_2[0] == -1 || temp_min_2[1] > current {
                temp_min_2 = []int{index, current}
            }
        }

        min_1 = temp_min_1
        min_2 = temp_min_2
    }

    return min_1[1]
}
```
