![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
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
