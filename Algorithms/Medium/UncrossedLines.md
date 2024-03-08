![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Uncrossed Lines](https://leetcode.com/problems/uncrossed-lines)

### Intuition :

uncrossed line equal to LCS (longest common subsequence) problem.

### Solution :

Method 1 (Divide & Conquer, ERROR: "Time Limit Exceeded") :
```rust
use std::cmp;
impl Solution {
    pub fn max_uncrossed_lines(nums1: Vec<i32>, nums2: Vec<i32>) -> i32 {
        let len_1 = nums1.len();
        let len_2 = nums2.len();
        let mut result = vec![vec![0; len_2+1]; len_1+1];
        Self::divide_conquer(len_1, len_2, &nums1, &nums2, &mut result)
    }

    fn divide_conquer(i: usize, j: usize, nums1: &Vec<i32>, nums2: &Vec<i32>, result: &mut Vec<Vec<i32>>) -> i32 {
        if i == 0 || j == 0 || i > nums1.len() || j > nums2.len() {
            return 0
        }
        if result[i][j] > 0 {
            return result[i][j]
        }

        match nums1[i-1] == nums2[j-1] {
            true => result[i][j] = Self::divide_conquer(i-1, j-1, nums1, nums2, result) + 1,
            false => result[i][j] = cmp::max(Self::divide_conquer(i-1, j, nums1, nums2, result), Self::divide_conquer(i, j-1, nums1, nums2, result)),
        }

        result[i][j]
    }
}
```

Method 2 (Dynamic Programming 2D, Top Down) :
```rust
use std::cmp;
use std::collections::HashMap;
impl Solution {
    pub fn max_uncrossed_lines(nums1: Vec<i32>, nums2: Vec<i32>) -> i32 {
        let len_1 = nums1.len();
        let len_2 = nums2.len();
        let mut result = HashMap::new();
        for index1 in 1..len_1+1 {
            for index2 in 1..len_2+1 {
                result.insert((index1, index2), -1);
            }
        }
        Self::dynamic_programming(len_1, len_2, &nums1, &nums2, &mut result)
    }

    // i, j mean to amount i and amount j, not index i and index j
    fn dynamic_programming(i: usize, j: usize, nums1: &Vec<i32>, nums2: &Vec<i32>, result: &mut HashMap<(usize, usize), i32>) -> i32 {
        if i == 0 || j == 0 || i > nums1.len() || j > nums2.len() {
            return 0
        }

        let &value = result.get(&(i, j)).unwrap();
        if value >= 0 {
            return value
        }

        let mut temp = 0;
        match nums1[i-1] == nums2[j-1] {
            true => temp = Self::dynamic_programming(i-1, j-1, nums1, nums2, result) + 1,
            false => temp = cmp::max(Self::dynamic_programming(i-1, j, nums1, nums2, result), Self::dynamic_programming(i, j-1, nums1, nums2, result)),
        };

        result.insert((i, j), temp);
        *result.get(&(i, j)).unwrap()
    }
}
```

Method 3 (Dynamic Programming 2D, Bottom Up) :
```rust
use std::cmp;
use std::collections::HashMap;
impl Solution {
    pub fn max_uncrossed_lines(nums1: Vec<i32>, nums2: Vec<i32>) -> i32 {
        let len_1 = nums1.len();
        let len_2 = nums2.len();
        Self::dynamic_programming(len_1, len_2, &nums1, &nums2)
    }

    fn dynamic_programming(i: usize, j: usize, nums1: &Vec<i32>, nums2: &Vec<i32>) -> i32 {
        if i < 0 || j < 0 || i > nums1.len() || j > nums2.len() {
            return 0
        }

        let mut result = HashMap::new();
        for index_i in 1..i+1 {
            for index_j in 1..j+1 {
                let mut temp = 0;
                match nums1[index_i-1] == nums2[index_j-1] {
                    true => temp = *result.get(&(index_i-1, index_j-1)).unwrap_or(&0) + 1,
                    false => temp = cmp::max(*result.get(&(index_i-1, index_j)).unwrap_or(&0), *result.get(&(index_i, index_j-1)).unwrap_or(&0)),
                };
                result.insert((index_i, index_j), temp);
            }
        }

        result[&(i, j)]
    }
}
```

Method 4 (Dynamic Programming, only use 2 rows, previous row and current row, to calculate LCS) :
```rust
use std::cmp;
impl Solution {
    pub fn max_uncrossed_lines(nums1: Vec<i32>, nums2: Vec<i32>) -> i32 {
        let len_1 = nums1.len();
        let len_2 = nums2.len();
        Self::dynamic_programming(len_1, len_2, &nums1, &nums2)
    }

    fn dynamic_programming(i: usize, j: usize, nums1: &Vec<i32>, nums2: &Vec<i32>) -> i32 {
        if i < 0 || j < 0 || i > nums1.len() || j > nums2.len() {
            return 0
        }

        let mut row_previous = vec![0; j+1];
        for index_i in 1..i+1 {
            let mut row_current = vec![0; j+1];
            for index_j in 1..j+1 {
                match nums1[index_i-1] == nums2[index_j-1] {
                    true => row_current[index_j] = row_previous[index_j-1] + 1,
                    false => row_current[index_j] = cmp::max(row_current[index_j-1], row_previous[index_j]),
                };
            }
            row_previous = row_current;
        }

        row_previous[j]
    }
}
```
