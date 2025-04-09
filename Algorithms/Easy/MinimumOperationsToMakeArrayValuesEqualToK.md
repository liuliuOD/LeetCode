![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3375. [Minimum Operations To Make Array Values Equal To K](https://leetcode.com/problems/minimum-operations-to-make-array-values-equal-to-k)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn min_operations(nums: Vec<i32>, k: i32) -> i32 {
        let mut result: i32 = 0;
        let mut visited: HashSet<i32> = HashSet::new();
        for &num in &nums {
            if visited.contains(&num) || num == k {
                continue;
            }

            if num < k {
                return -1
            }

            visited.insert(num);
            result += 1;
        }

        return result
    }
}
```

Method 2 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn min_operations(mut nums: Vec<i32>, k: i32) -> i32 {
        nums.sort();
        nums.dedup();
        if nums[0] < k {
            return -1
        } else if nums[0] == k {
            return nums.len() as i32 - 1
        }

        return nums.len() as i32
    }
}
```
