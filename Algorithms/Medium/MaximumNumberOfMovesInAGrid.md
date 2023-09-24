![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
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

### Solution :

Method 1 (DFS + Memoization) :
```php
class Solution {

    /**
     * @param Integer[][] $grid
     * @return Integer
     */
    function maxMoves($grid) {
        $this->m = count($grid);
        $this->n = count($grid[0]);

        $memoization = array_fill(0, $this->m, array_fill(0, $this->n, -1));
        $result = 0;
        for ($index = 0; $index < $this->m; $index++) {
            $result = max($result, $this->dfs($index, 0, $memoization, $grid));
        }

        return $result;
    }

    function dfs($x, $y, &$memoization, $grid) : Int {
        if ($memoization[$x][$y] != -1) {
            return $memoization[$x][$y];
        }

        $result = 0;
        foreach([[$x-1, $y+1], [$x, $y+1], [$x+1, $y+1]] as list($xNext, $yNext)) {
            if ($xNext >= $this->m || $xNext < 0 || $yNext >= $this->n || $yNext < 0) {
                continue;
            }

            if ($grid[$x][$y] >= $grid[$xNext][$yNext]) {
                continue;
            }

            $result = max($result, 1 + $this->dfs($xNext, $yNext, $memoization, $grid));
        }

        return $memoization[$x][$y] = $result;
    }
}
```
