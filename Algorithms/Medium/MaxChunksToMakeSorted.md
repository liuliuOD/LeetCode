![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 769. [Max Chunks To Make Sorted](https://leetcode.com/problems/max-chunks-to-make-sorted)

### Solution :

Method 1 (Prefix + Suffix, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `arr`)) :
```rust
impl Solution {
    pub fn max_chunks_to_sorted(arr: Vec<i32>) -> i32 {
        let n: usize = arr.len();
        let mut prefix_maximum: Vec<i32> = arr.clone();
        let mut suffix_minimum: Vec<i32> = arr.clone();
        for index in 1..n {
            prefix_maximum[index] = i32::max(prefix_maximum[index-1], prefix_maximum[index]);
        }
        for index in (0..n-1).rev() {
            suffix_minimum[index] = i32::min(suffix_minimum[index], suffix_minimum[index+1]);
        }

        let mut result: i32 = 1;
        for index in 1..n {
            if prefix_maximum[index-1] <= suffix_minimum[index] {
                result += 1;
            }
        }

        return result
    }
}
```
