![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1671. [Minimum Number Of Removals To Make Mountain Array](https://leetcode.com/problems/minimum-number-of-removals-to-make-mountain-array)

### Solution :

Method 1 (DFS, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn minimum_mountain_removals(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut counter_strictly_increment: Vec<i32> = vec![0; n];
        for index in 1..n {
            for index_previous in 0..index {
                if nums[index] > nums[index_previous] {
                    counter_strictly_increment[index] = *[counter_strictly_increment[index], counter_strictly_increment[index_previous] + 1, 2].iter().max().unwrap();
                }
            }
        }

        let mut counter_strictly_decrement: Vec<i32> = vec![0; n];
        for index in (0..n-1).rev() {
            for index_next in index+1..n {
                if nums[index] > nums[index_next] {
                    counter_strictly_decrement[index] = *[counter_strictly_decrement[index], counter_strictly_decrement[index_next] + 1, 2].iter().max().unwrap();
                }
            }
        }

        let mut length_maximum_mountain_array: i32 = 0;
        for index in 1..n-1 {
            if counter_strictly_increment[index] <= 0 || counter_strictly_decrement[index] <= 0 {
                continue;
            }

            length_maximum_mountain_array = i32::max(length_maximum_mountain_array, counter_strictly_increment[index]+counter_strictly_decrement[index]-1);
        }

        return n as i32 - length_maximum_mountain_array
    }
}
```
