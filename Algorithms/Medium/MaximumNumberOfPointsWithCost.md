![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1937. [Maximum Number Of Points With Cost](https://leetcode.com/problems/maximum-number-of-points-with-cost)

### Solution :

Method 1 (Dynamic Programming, ERROR: "Time Limit Exceeded", 152/157, Time Complexity: $O(M*N^2)$, Space Complexity: $O(M*N)$) :
```rust
impl Solution {
    pub fn max_points(points: Vec<Vec<i32>>) -> i64 {
        let m: usize = points.len();
        let n: usize = points[0].len();
        let mut dp: Vec<Vec<i64>> = vec![vec![0; n]; m];
        for index_m in (0..m).rev() {
            for index_n in 0..n {
                if index_m == m-1 {
                    dp[index_m][index_n] = points[index_m][index_n] as i64;
                    continue;
                }

                for index_n_next_row in 0..n {
                    dp[index_m][index_n] = dp[index_m][index_n].max(points[index_m][index_n] as i64+dp[index_m+1][index_n_next_row]-(index_n as i64-index_n_next_row as i64).abs());
                }
            }
        }

        return *dp[0].iter().max().unwrap()
    }
}
```

Method 2 (Dynamic Programming, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```rust
impl Solution {
    pub fn max_points(points: Vec<Vec<i32>>) -> i64 {
        let m: usize = points.len();
        let n: usize = points[0].len();
        let mut dp: Vec<Vec<i64>> = vec![vec![0; n]; m];
        dp[m-1] = points[m-1].iter().map(|value| *value as i64).collect();

        for index_m in (0..m-1).rev() {
            let mut maximum_left: Vec<i64> = vec![0; n];
            maximum_left[0] = dp[index_m+1][0];
            for index_n in 1..n {
                maximum_left[index_n] = (maximum_left[index_n-1]-1).max(dp[index_m+1][index_n]);
            }

            let mut maximum_right: Vec<i64> = vec![0; n];
            maximum_right[n-1] = dp[index_m+1][n-1];
            for index_n in (0..n-1).rev() {
                maximum_right[index_n] = (maximum_right[index_n+1]-1).max(dp[index_m+1][index_n]);
            }

            for index_n in 0..n {
                dp[index_m][index_n] = points[index_m][index_n] as i64 + i64::max(maximum_left[index_n], maximum_right[index_n]);
            }
        }

        return *dp[0].iter().max().unwrap()
    }
}
```

Method 3 (Dynamic Programming + Optimization, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn max_points(points: Vec<Vec<i32>>) -> i64 {
        let m: usize = points.len();
        let n: usize = points[0].len();
        let mut dp: Vec<i64> = points[m-1].iter().map(|value| *value as i64).collect();

        for index_m in (0..m-1).rev() {
            let mut current_points: Vec<i64> = vec![0; n];
            let mut maximum_left: Vec<i64> = vec![0; n];
            maximum_left[0] = dp[0];
            for index_n in 1..n {
                maximum_left[index_n] = (maximum_left[index_n-1]-1).max(dp[index_n]);
            }

            let mut maximum_right: Vec<i64> = vec![0; n];
            maximum_right[n-1] = dp[n-1];
            for index_n in (0..n-1).rev() {
                maximum_right[index_n] = (maximum_right[index_n+1]-1).max(dp[index_n]);
            }

            for index_n in 0..n {
                current_points[index_n] = points[index_m][index_n] as i64 + i64::max(maximum_left[index_n], maximum_right[index_n]);
            }

            dp = current_points;
        }

        return *dp.iter().max().unwrap()
    }
}
```
