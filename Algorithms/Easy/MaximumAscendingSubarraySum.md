![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1800. [Maximum Ascending Subarray Sum](https://leetcode.com/problems/maximum-ascending-subarray-sum)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: number of elements in `nums`)) :
```Rust
impl Solution {
    pub fn max_ascending_sum(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut sum: i32 = nums[0];
        let mut result: i32 = sum;
        for index in 0..n-1 {
            /* Option 1 */
            if nums[index] < nums[index+1] {
                sum += nums[index+1];
            } else {
                sum = nums[index+1];
            }
            /* Option 2

            if nums[index] >= nums[index+1] {
                sum = 0;
            }
            sum += nums[index+1];
            */

            result = i32::max(result, sum);
        }

        return result
    }
}
```
