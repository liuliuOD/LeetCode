![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 463. [Island Perimeter](https://leetcode.com/problems/island-perimeter)

### Solution :

Method 1 (Stack, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```rust
impl Solution {
    pub fn island_perimeter(mut grid: Vec<Vec<i32>>) -> i32 {
        let mut stack: Vec<(usize, usize)> = vec![];
        for (index_m, row) in grid.iter().enumerate() {
            for (index_n, &item) in row.iter().enumerate() {
                if item == 1 {
                    stack.push((index_m, index_n));
                    break;
                }
            }
        }

        let m: usize = grid.len();
        let n: usize = grid[0].len();
        let mut amount: i32 = 0;
        let mut connected_amount: i32 = 0;
        while stack.len() > 0 {
            let (index_m, index_n) = stack.pop().unwrap();
            if grid[index_m][index_n] == 0 {
                continue
            }
            grid[index_m][index_n] = 0;
            amount += 1;

            if 0 <= index_m - 1 && index_m - 1 < m && grid[index_m-1][index_n] == 1 {
                connected_amount += 1;
                stack.push((index_m-1, index_n));
            }
            if index_m + 1 < m && grid[index_m+1][index_n] == 1 {
                connected_amount += 1;
                stack.push((index_m+1, index_n));
            }
            if 0 <= index_n - 1 && index_n - 1 < n && grid[index_m][index_n-1] == 1 {
                connected_amount += 1;
                stack.push((index_m, index_n-1));
            }
            if index_n + 1 < n && grid[index_m][index_n+1] == 1 {
                connected_amount += 1;
                stack.push((index_m, index_n+1));
            }
        }

        return amount * 4 - connected_amount * 2
    }
}
```

Method 2 (Traverse, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn island_perimeter(grid: Vec<Vec<i32>>) -> i32 {
        let mut result : i32 = 0;
        let m: usize = grid.len();
        let n: usize = grid[0].len();
        for index_m in 0..m {
            for index_n in 0..n {
                if grid[index_m][index_n] == 0 {
                    continue;
                }

                for (offset_m, offset_n) in [(0, -1), (0, 1), (-1, 0), (1, 0)] {
                    let index_m_next: usize = ((index_m as i32) + offset_m) as usize;
                    let index_n_next: usize = ((index_n as i32) + offset_n) as usize;
                    if index_m_next < m && index_n_next < n {
                        match grid[index_m_next][index_n_next] {
                            0 => result += 1,
                            _ => (),
                        };
                    } else {
                        result += 1;
                    }
                }
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Traverse, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        result: int = 0
        for index_m in range(m):
            for index_n in range(n):
                if grid[index_m][index_n] == 0:
                    continue

                for offset_m, offset_n in [(0, -1), (0, 1), (-1, 0), (1, 0)]:
                    index_m_next = index_m+offset_m
                    index_n_next = index_n+offset_n
                    if 0 <= index_m_next < m and 0 <= index_n_next < n:
                        result += int(grid[index_m_next][index_n_next] == 0)
                    else:
                        result += 1

        return result
```
