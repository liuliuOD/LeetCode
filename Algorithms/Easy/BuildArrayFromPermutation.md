![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1920. [Build Array From Permutation](https://leetcode.com/problems/build-array-from-permutation)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn build_array(nums: Vec<i32>) -> Vec<i32> {
        let n: usize = nums.len();
        let mut result: Vec<i32> = vec![0; n];
        for (index, &num) in nums.iter().enumerate() {
            result[index] = nums[num as usize];
        }

        return result
    }
}
```
