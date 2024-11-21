![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2257. [Count Unguarded Cells In The Grid](https://leetcode.com/problems/count-unguarded-cells-in-the-grid)

### Solution :

Method 1 (Brute Force + Hash Set, ERROR: "Time Limit Exceeded", 38/48, Time Complexity: $O(M*N+K*(M+N))$, Space Complexity: $O(M*N)$ (M: the value of `m`, N: the value of `n`, K: the number of the elements in `guards`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn count_unguarded(m: i32, n: i32, guards: Vec<Vec<i32>>, walls: Vec<Vec<i32>>) -> i32 {
        let m: usize = m as usize;
        let n: usize = n as usize;
        let mut mapping: Vec<Vec<bool>> = vec![vec![true; n]; m];
        let mut walls_set: HashSet<(usize, usize)> = HashSet::new();
        for wall in walls {
            walls_set.insert((wall[0] as usize, wall[1] as usize));
        }

        for guard in guards {
            let x: usize = guard[0] as usize;
            let y: usize = guard[1] as usize;
            mapping[x][y] = false;

             let mut x_previous: usize = x;
             while x_previous > 0 &&!walls_set.contains(&(x_previous-1, y)) {
                mapping[x_previous-1][y] = false;
                x_previous -= 1;
             }

             let mut x_next: usize = x;
             while x_next < m-1 &&!walls_set.contains(&(x_next+1, y)) {
                mapping[x_next+1][y] = false;
                x_next += 1;
             }

             let mut y_previous: usize = y;
             while y_previous > 0 &&!walls_set.contains(&(x, y_previous-1)) {
                mapping[x][y_previous-1] = false;
                y_previous -= 1;
             }

             let mut y_next: usize = y;
             while y_next < n-1 &&!walls_set.contains(&(x, y_next+1)) {
                mapping[x][y_next+1] = false;
                y_next += 1;
             }
        }

        let mut result: i32 = 0;
        for index_m in 0..m {
            for index_n in 0..n {
                if mapping[index_m][index_n] {
                    result += 1;
                }
            }
        }

        return result - walls_set.len() as i32
    }
}
```

Method 2 (Brute Force + Hash Set + Optimization, Time Complexity: $O(M*N+K*(M+N))$, Space Complexity: $O(M*N)$ (M: the value of `m`, N: the value of `n`, K: the number of the elements in `guards`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn count_unguarded(m: i32, n: i32, guards: Vec<Vec<i32>>, walls: Vec<Vec<i32>>) -> i32 {
        let m: usize = m as usize;
        let n: usize = n as usize;
        let mut mapping: Vec<Vec<bool>> = vec![vec![true; n]; m];
        let mut walls_set: HashSet<(usize, usize)> = HashSet::new();
        for wall in walls {
            walls_set.insert((wall[0] as usize, wall[1] as usize));
        }
        let mut guards_set: HashSet<(usize, usize)> = HashSet::new();
        for guard in guards {
            guards_set.insert((guard[0] as usize, guard[1] as usize));
        }

        for guard in guards_set.iter() {
            let x: usize = guard.0 as usize;
            let y: usize = guard.1 as usize;
            mapping[x][y] = false;

             let mut x_previous: usize = x;
             while x_previous > 0 && !walls_set.contains(&(x_previous-1, y)) && !guards_set.contains(&(x_previous-1, y)) {
                mapping[x_previous-1][y] = false;
                x_previous -= 1;
             }

             let mut x_next: usize = x;
             while x_next < m-1 && !walls_set.contains(&(x_next+1, y)) && !guards_set.contains(&(x_next+1, y)) {
                mapping[x_next+1][y] = false;
                x_next += 1;
             }

             let mut y_previous: usize = y;
             while y_previous > 0 && !walls_set.contains(&(x, y_previous-1)) && !guards_set.contains(&(x, y_previous-1)) {
                mapping[x][y_previous-1] = false;
                y_previous -= 1;
             }

             let mut y_next: usize = y;
             while y_next < n-1 && !walls_set.contains(&(x, y_next+1)) && !guards_set.contains(&(x, y_next+1)) {
                mapping[x][y_next+1] = false;
                y_next += 1;
             }
        }

        let mut result: i32 = 0;
        for index_m in 0..m {
            for index_n in 0..n {
                if mapping[index_m][index_n] {
                    result += 1;
                }
            }
        }

        return result - walls_set.len() as i32
    }
}
```
