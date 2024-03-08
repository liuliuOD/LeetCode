![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Spiral Matrix](https://leetcode.com/problems/spiral-matrix)

### Solution :

Method 1 (Brute Force, using data structure *Set* to store been traversed points, and change direction in 4 modes) :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn spiral_order(matrix: Vec<Vec<i32>>) -> Vec<i32> {
        let mut hs: HashSet<(usize, usize)> = HashSet::new();
        let mut result = vec![];
        let matrix_amount = matrix.len() * matrix[0].len();
        let mut i = 0;
        let mut j = 0;
        let mut mode = 0;
        while hs.len() < matrix_amount {
            match mode {
                0 => {
                    if j == matrix[0].len() || hs.contains(&(i, j)) {
                        mode += 1;
                        i += 1;
                        j -= 1;
                        continue;
                    }
                    result.push(matrix[i][j]);
                    hs.insert((i, j));
                    j += 1;
                },
                1 => {
                    if i == matrix.len() || hs.contains(&(i, j)) {
                        mode += 1;
                        i -= 1;
                        j -= 1;
                        continue;
                    }
                    result.push(matrix[i][j]);
                    hs.insert((i, j));
                    i += 1;
                },
                2 => {
                    if j > matrix[0].len() || hs.contains(&(i, j)) {
                        mode += 1;
                        i -= 1;
                        if j > matrix[0].len() {
                            j = 0;
                        } else {
                            j += 1;
                        }
                        continue;
                    }
                    result.push(matrix[i][j]);
                    hs.insert((i, j));
                    j -= 1;
                },
                3 => {
                    if hs.contains(&(i, j)) {
                        mode = 0;
                        i += 1;
                        j += 1;
                        continue;
                    }
                    result.push(matrix[i][j]);
                    hs.insert((i, j));
                    i -= 1;
                },
                _ => (),
            }
        }
        result
    }
}
```

Method 2 (DFS) :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn spiral_order(matrix: Vec<Vec<i32>>) -> Vec<i32> {
        let mut result = vec![];
        let mut hs: HashSet<(usize, usize)> = HashSet::new();
        Self::dfs(0, 0, 0, &matrix, &mut hs, &mut result);

        result
    }

    fn dfs(i: usize, j: usize, mode: usize, matrix: &Vec<Vec<i32>>, hs: &mut HashSet<(usize, usize)>, result: &mut Vec<i32>) {
        if hs.contains(&(i, j)) || i < 0 || j < 0 || i >= matrix.len() || j >= matrix[0].len() {
            return
        }
        hs.insert((i, j));
        result.push(matrix[i][j]);

        // order: right -> bottom -> left -> top
        let traverse_order = vec![(i, j+1), (i+1, j), (i, j-1), (i-1, j)];
        let mut traverse_mode = mode;
        while traverse_mode < traverse_order.len() {
            Self::dfs(traverse_order[traverse_mode].0, traverse_order[traverse_mode].1, traverse_mode, matrix, hs, result);

            traverse_mode += 1;

            // when there are other points unvisited, we need to keep traversing
            if traverse_mode >= traverse_order.len() && hs.len() < matrix.len() * matrix[0].len() {
                traverse_mode = 0;
            }
        }
    }
}
```

Method 3 (DFS, modify values in matrix to prevent storing in HashSet) :
```rust
const VISITED: i32 = -101;
impl Solution {
    pub fn spiral_order(mut matrix: Vec<Vec<i32>>) -> Vec<i32> {
        let mut result = vec![];
        Self::dfs(0, 0, 0, &mut matrix, &mut result);

        result
    }

    fn dfs(i: usize, j: usize, mode: usize, matrix: &mut Vec<Vec<i32>>, result: &mut Vec<i32>) {
        if i < 0 || j < 0 || i >= matrix.len() || j >= matrix[0].len() || matrix[i][j] == VISITED {
            return
        }
        result.push(matrix[i][j]);
        matrix[i][j] = VISITED;

        let traverse_order = vec![(i, j+1), (i+1, j), (i, j-1), (i-1, j)];
        let mut traverse_mode = mode;
        loop {
            Self::dfs(traverse_order[traverse_mode].0, traverse_order[traverse_mode].1, traverse_mode, matrix, result);

            traverse_mode += 1;
            if traverse_mode >= traverse_order.len() && result.len() < matrix.len() * matrix[0].len() {
                traverse_mode = 0;
            } else if traverse_mode == traverse_order.len() {
                break;
            }
        }
    }
}
```
