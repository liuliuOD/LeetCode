![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2033. [Minimum Operations To Make A Uni-Value Grid](https://leetcode.com/problems/minimum-operations-to-make-a-uni-value-grid)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 37/62, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$ (M: the difference between maximum and minimum elements in `grid`, N: the number of elements in `grid`)) :
```rust
impl Solution {
    pub fn min_operations(grid: Vec<Vec<i32>>, x: i32) -> i32 {
        let mut nums: Vec<i32> = Vec::new();
        let mut minimum: i32 = i32::MAX;
        let mut maximum: i32 = i32::MIN;
        for row in grid {
            for num in row {
                minimum = i32::min(minimum, num);
                maximum = i32::max(maximum, num);
                nums.push(num);
            }
        }

        let mut result: i32 = i32::MAX;
        for target in minimum..=maximum {
            let mut temp: i32 = 0;
            for num in &nums {
                let diff: i32 = (num-target).abs();
                if diff%x != 0 {
                    temp = i32::MAX;
                    break;
                }

                temp += diff / x;
            }

            result = i32::min(result, temp);
        }

        return match result {
            i32::MAX => -1,
            _ => result,
        }
    }
}
```
