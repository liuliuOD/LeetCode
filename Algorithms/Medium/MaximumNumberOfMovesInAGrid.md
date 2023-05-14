![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2684. [Maximum Number Of Moves In A Grid](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid)

### Solution :

Method 1 (In weekly contest 345) :
```rust
use std::cmp::max;
use std::collections::HashMap;
impl Solution {
    pub fn max_moves(grid: Vec<Vec<i32>>) -> i32 {
        let mut hm: HashMap<(usize, usize), i32> = HashMap::new();

        for i in 0..grid.len() {
            Self::dfs(i, 0, 0, &grid, &mut hm);
        }

        let mut result = i32::MIN;
        for i in 0..grid.len() {
            if *hm.get(&(i, 0)).unwrap() > result {
                result = *hm.get(&(i, 0)).unwrap();
            }
        }
        result
    }
    
    fn dfs(i: usize, j: usize, current: i32, grid: &Vec<Vec<i32>>, hm: &mut HashMap<(usize, usize), i32>) -> i32 {
        if i <0 || j <0 || i >=grid.len() || j >= grid[0].len() || current >= grid[i][j] {
            return 0
        }
        
        if hm.contains_key(&(i, j)) {
            return *hm.get(&(i, j)).unwrap()
        }
        
        let current = grid[i][j];
        let mut temp = max(max(Self::dfs(i-1, j+1, current, grid, hm), Self::dfs(i, j+1, current, grid, hm)), Self::dfs(i+1, j+1, current, grid, hm));
        hm.insert((i, j), temp);
        
        return temp + 1
    }
}
```
