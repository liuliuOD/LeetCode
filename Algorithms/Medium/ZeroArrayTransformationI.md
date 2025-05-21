![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3355. [Zero Array Transformation I](https://leetcode.com/problems/zero-array-transformation-i)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `queries`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn is_zero_array(nums: Vec<i32>, queries: Vec<Vec<i32>>) -> bool {
        let n: usize = nums.len();
        let mut incrementer: Vec<i32> = vec![0; n+1];
        for pair in queries {
            let left: usize = pair[0] as usize;
            let right: usize = pair[1] as usize;
            incrementer[left] += 1;
            incrementer[right+1] -= 1;
        }

        let mut current: i32 = 0;
        for index in 0..n {
            current += incrementer[index];
            if current < nums[index] {
                return false
            }
        }

        return true
    }
}
```
