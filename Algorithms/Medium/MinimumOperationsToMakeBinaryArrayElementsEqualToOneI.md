![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3191. [Minimum Operations To Make Binary Array Elements Equal To One I](https://leetcode.com/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn min_operations(mut nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut index: usize = 0;
        let mut result: i32 = 0;
        while index < n {
            if nums[index] == 0 {
                if index+2 >= n {
                    return -1
                }

                for offset in 0..3 {
                    nums[index+offset] = (nums[index+offset]+1)%2;
                }
                result += 1;
            }

            index += 1;
        }

        return result
    }
}
```

Method 2 (Brute Force + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn min_operations(mut nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut index: usize = 0;
        let mut result: i32 = 0;
        while index < n {
            if nums[index] == 1 {
                index += 1;
                continue;
            }

            if index+2 >= n {
                return -1
            }

            let mut index_next: usize = index;
            for offset in 0..3 {
                nums[index+offset] = (nums[index+offset]+1)%2;
                if nums[index+offset] == 0 && index_next == index {
                    index_next = index + offset;
                }
            }
            result += 1;
            index = index_next;
        }

        return result
    }
}
```
