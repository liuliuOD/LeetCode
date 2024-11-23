![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1861. [Rotating The Box](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows)

### Solution :

Method 1 (Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```rust
impl Solution {
    pub fn rotate_the_box(matrix: Vec<Vec<char>>) -> Vec<Vec<char>> {
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut result: Vec<Vec<char>> = vec![vec!['.'; m]; n];
        for index_m in 0..m {
            let mut amount_stone: usize = 0;
            for index_n in 0..n {
                match matrix[index_m][index_n] {
                    '#' => {
                        amount_stone += 1;
                        if index_n == n-1 {
                            for offset in 0..amount_stone {
                                result[index_n-offset][m-index_m-1] = '#';
                            }
                        }
                    },
                    '*' => {
                        result[index_n][m-index_m-1] = '*';
                        for offset in 1..=amount_stone {
                            result[index_n-offset][m-index_m-1] = '#';
                        }

                        amount_stone = 0;
                    },
                    '.' if index_n == n-1 => {
                        for offset in 0..amount_stone {
                            result[index_n-offset][m-index_m-1] = '#';
                        }
                    },
                    '.' | _ => {},
                };
            }
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```rust
impl Solution {
    pub fn rotate_the_box(matrix: Vec<Vec<char>>) -> Vec<Vec<char>> {
        let m: usize = matrix.len();
        let n: usize = matrix[0].len();
        let mut result: Vec<Vec<char>> = vec![vec!['.'; m]; n];
        for index_m in 0..m {
            let mut amount_stone: usize = 0;
            for index_n in 0..n {
                match matrix[index_m][index_n] {
                    '#' => {
                        amount_stone += 1;
                    },
                    '*' => {
                        result[index_n][m-index_m-1] = '*';
                        while amount_stone > 0 {
                            result[index_n-amount_stone][m-index_m-1] = '#';
                            amount_stone -= 1
                        }

                        amount_stone = 0;
                    },
                    '.' | _ => {},
                };
            }

            for offset in 0..amount_stone {
                result[n-offset-1][m-index_m-1] = '#';
            }
        }

        return result
    }
}
```
