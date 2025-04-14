![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1534. [Count Good Triplets](https://leetcode.com/problems/count-good-triplets)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^3)$, Space Complexity: $O(1)$ (N: the number of elements in `arr`)) :
```rust
impl Solution {
    pub fn count_good_triplets(arr: Vec<i32>, a: i32, b: i32, c: i32) -> i32 {
        let n: usize = arr.len();
        let mut result: i32 = 0;
        for index_i in 0..n {
            for index_j in index_i+1..n {
                for index_k in index_j+1..n {
                    if i32::abs(arr[index_i]-arr[index_j]) <= a && i32::abs(arr[index_j]-arr[index_k]) <= b && i32::abs(arr[index_i]-arr[index_k]) <= c {
                        result += 1;
                    }
                }
            }
        }

        return result
    }
}
```
