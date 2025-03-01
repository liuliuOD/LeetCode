![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2460. [Apply Operations To An Array](https://leetcode.com/problems/apply-operations-to-an-array)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn apply_operations(mut nums: Vec<i32>) -> Vec<i32> {
        let n: usize = nums.len();
        let mut amount_zero: usize = 0;
        let mut result: Vec<i32> = Vec::new();
        for index in 0..n-1 {
            let current: i32 = nums[index];
            if current == 0 || current != nums[index+1] {
                if current == 0 {
                    amount_zero += 1;
                } else {
                    result.push(current);
                }

                continue;
            }

            nums[index+1] = 0;
            result.push(current*2);
        }

        if nums[n-1] == 0 {
            amount_zero += 1;
        } else {
            result.push(nums[n-1]);
        }
        for _ in 0..amount_zero {
            result.push(0);
        }

        return result
    }
}
```
