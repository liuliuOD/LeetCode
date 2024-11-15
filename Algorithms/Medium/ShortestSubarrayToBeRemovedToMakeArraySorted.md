![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1574. [Shortest Subarray To Be Removed To Make Array Sorted](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn find_length_of_shortest_subarray(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut index_right: usize = n - 1;
        while index_right > 0 && nums[index_right-1] <= nums[index_right] {
            index_right -= 1;
        }

        let mut result: i32 = index_right as i32;
        let mut index_left: usize = 0;
        while index_left < index_right && (index_left == 0 || nums[index_left-1] <= nums[index_left]) {
            while index_right < n && nums[index_left] > nums[index_right] {
                index_right += 1;
            }

            result = i32::min(result, (index_right-index_left-1) as i32);
            index_left += 1;
        }

        return result
    }
}
```
