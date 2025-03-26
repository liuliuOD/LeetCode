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

Method 2 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of elements in `grid`)) :
```rust
impl Solution {
    pub fn min_operations(grid: Vec<Vec<i32>>, x: i32) -> i32 {
        let mut nums: Vec<i32> = grid.into_iter().flat_map(|row| row).collect();
        nums.sort_unstable(); // Sort the flattened array

        let n = nums.len();
        if n == 1 {
            return 0; // Single element is already uniform
        }

        // Check if all differences from the first element are divisible by x
        for i in 1..n {
            let diff = (nums[i] - nums[0]).abs();
            if diff % x != 0 {
                return -1; // Impossible if any difference isn't a multiple of x
            }
        }

        // Use median as target to minimize operations
        let median = nums[n / 2]; // Middle element after sorting
        let mut operations: i64 = 0;

        // Calculate total operations to reach median
        for &num in &nums {
            operations += ((num - median).abs() / x) as i64;
        }

        return operations as i32
    }
}
```
