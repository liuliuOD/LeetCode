![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3024. [Type Of Triangle](https://leetcode.com/problems/type-of-triangle)

### Solution :

Method 1 (Greedy, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn triangle_type(nums: Vec<i32>) -> String {
        let sum_total: i32 = nums.iter().sum();
        for index_a in 0..3 {
            for index_b in index_a+1..3 {
                let sum_current: i32 = nums[index_a] + nums[index_b];
                let side_c: i32 = sum_total - sum_current;
                if sum_current <= side_c {
                    return "none".to_string()
                }

                if nums[index_a] == nums[index_b] {
                    if nums[index_a] == side_c {
                        return "equilateral".to_string()
                    }
                    return "isosceles".to_string()
                }
            }
        }

        return "scalene".to_string()
    }
}
```
