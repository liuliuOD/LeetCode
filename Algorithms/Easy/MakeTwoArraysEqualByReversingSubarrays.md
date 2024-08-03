![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1460. [Make Two Arrays Equal By Reversing Subarrays](https://leetcode.com/problems/make-two-arrays-equal-by-reversing-subarrays)

### Solution :

Method 1 (Sorted, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: number of the elements in `target`)) :
```rust
impl Solution {
    pub fn can_be_equal(mut target: Vec<i32>, mut arr: Vec<i32>) -> bool {
        target.sort();
        arr.sort();
        for (a, b) in target.iter().zip(arr.iter()) {
            if a != b {
                return false
            }
        }

        return true
    }
}
```
