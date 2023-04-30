## [Maximum Number Of Fish In A Grid](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid)

### Solution :

Method 1 (In biweely contest 103 (keep the original input)):
```rust
impl Solution {
    pub fn find_max_fish(mut grid: Vec<Vec<i32>>) -> i32 {
        let mut visited = vec![vec![false; grid[0].len()]; grid.len()];
        let mut result = 0;
        for i in 0..grid.len() {
            for j in 0..grid[i].len() {
                if visited[i][j] || grid[i][j] <= 0 {
                    continue;
                }
                
                visited[i][j] = true;
                let mut tempo = grid[i][j];
                Self::fishing(&mut visited, i, j, &mut grid, &mut tempo);
                result = std::cmp::max(result, tempo);
            }
        }
        
        result
    }
    
    pub fn fishing(mut visited: &mut Vec<Vec<bool>>, i: usize, j: usize, mut grid: &mut Vec<Vec<i32>>, mut tempo: &mut i32) {
        if i != 0 {
            if !visited[i-1][j] {
                visited[i-1][j] = true;
                if grid[i-1][j] > 0 {
                    *tempo += grid[i-1][j];
                    Self::fishing(&mut visited, i - 1, j, &mut grid, &mut tempo);
                }
            }
        }
        if j != 0 {
            if !visited[i][j-1] {
                visited[i][j-1] = true;
                if grid[i][j-1] > 0 {
                    *tempo += grid[i][j-1];
                    Self::fishing(&mut visited, i, j - 1, &mut grid, &mut tempo);
                }
            }
        }
        if i != grid.len() - 1 {
            if !visited[i+1][j] {
                visited[i+1][j] = true;
                if grid[i+1][j] > 0 {
                    *tempo += grid[i+1][j];
                    Self::fishing(&mut visited, i + 1, j, &mut grid, &mut tempo);
                }
            }
        }
        if j != grid[0].len() - 1 {
            if !visited[i][j+1] {
                visited[i][j+1] = true;
                if grid[i][j+1] > 0 {
                    *tempo += grid[i][j+1];
                    Self::fishing(&mut visited, i, j + 1, &mut grid, &mut tempo);
                }
            }
        }
    }
}
```

Method 2 (keep the original input) :
```rust
impl Solution {
    pub fn find_max_fish(mut grid: Vec<Vec<i32>>) -> i32 {
        let mut visited = vec![vec![false; grid[0].len()]; grid.len()];
        let mut result = 0;
        for i in 0..grid.len() {
            for j in 0..grid[i].len() {
                let mut tempo = 0;
                Self::fishing(&mut visited, i, j, &mut grid, &mut tempo);
                result = std::cmp::max(result, tempo);
            }
        }
        
        result
    }
    
    pub fn fishing(mut visited: &mut Vec<Vec<bool>>, i: usize, j: usize, mut grid: &mut Vec<Vec<i32>>, mut tempo: &mut i32) {
        if visited[i][j] || grid[i][j] <= 0 {
            return
        }

        *tempo += grid[i][j];
        visited[i][j] = true;

        if i > 0 {
            Self::fishing(&mut visited, i - 1, j, &mut grid, &mut tempo);
        }
        if j > 0 {
            Self::fishing(&mut visited, i, j - 1, &mut grid, &mut tempo);
        }
        if i < grid.len() - 1 {
            Self::fishing(&mut visited, i + 1, j, &mut grid, &mut tempo);
        }
        if j < grid[0].len() - 1 {
            Self::fishing(&mut visited, i, j + 1, &mut grid, &mut tempo);
        }
    }
}
```

Method 3 (keep the original input) :
```rust
impl Solution {
    pub fn find_max_fish(mut grid: Vec<Vec<i32>>) -> i32 {
        let mut visited = vec![vec![false; grid[0].len()]; grid.len()];
        let mut result = 0;
        for i in 0..grid.len() {
            for j in 0..grid[i].len() {
                result = std::cmp::max(result, Self::fishing(&mut visited, i, j, &mut grid));
            }
        }
        
        result
    }
    
    pub fn fishing(mut visited: &mut Vec<Vec<bool>>, i: usize, j: usize, mut grid: &mut Vec<Vec<i32>>) -> i32 {
        if i >= grid.len() || j >= grid[0].len() || visited[i][j] || grid[i][j] <= 0 {
            return 0
        }
        visited[i][j] = true;

        Self::fishing(&mut visited, i - 1, j, &mut grid) +
        Self::fishing(&mut visited, i, j - 1, &mut grid) +
        Self::fishing(&mut visited, i + 1, j, &mut grid) +
        Self::fishing(&mut visited, i, j + 1, &mut grid) + grid[i][j]
    }
}
```

Method 4 :
```rust
impl Solution {
    pub fn find_max_fish(mut grid: Vec<Vec<i32>>) -> i32 {
        let mut result = 0;
        for i in 0..grid.len() {
            for j in 0..grid[i].len() {
                let mut total_fishes = 0;
                let mut stack = vec![(i, j)];
                while stack.len() > 0 {
                    if let Some((position_i, position_j)) = stack.pop() {
                        if position_i >= grid.len() || position_j >= grid[0].len() || grid[position_i][position_j] <= 0 {
                            continue
                        }

                        total_fishes += grid[position_i][position_j];
                        grid[position_i][position_j] = 0;

                        stack.push((position_i + 1, position_j));
                        stack.push((position_i - 1, position_j));
                        stack.push((position_i, position_j + 1));
                        stack.push((position_i, position_j - 1));
                    }
                }

                result = std::cmp::max(result, total_fishes);
            }
        }
        
        result
    }
}
```

Method 5 (keep the original input) :
```rust
impl Solution {
    pub fn find_max_fish(mut grid: Vec<Vec<i32>>) -> i32 {
        let mut visited = vec![vec![false; grid[0].len()]; grid.len()];
        let mut result = 0;
        for i in 0..grid.len() {
            for j in 0..grid[i].len() {
                let mut total_fishes = 0;
                let mut stack = vec![(i, j)];
                while stack.len() > 0 {
                    if let Some((position_i, position_j)) = stack.pop() {
                        if position_i >= grid.len() || position_j >= grid[0].len() || visited[position_i][position_j] || grid[position_i][position_j] <= 0 {
                            continue
                        }

                        total_fishes += grid[position_i][position_j];
                        visited[position_i][position_j] = true;

                        stack.push((position_i + 1, position_j));
                        stack.push((position_i - 1, position_j));
                        stack.push((position_i, position_j + 1));
                        stack.push((position_i, position_j - 1));
                    }
                }

                result = std::cmp::max(result, total_fishes);
            }
        }
        
        result
    }
}
```
