![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2874. [Maximum Value Of An Ordered Triplet II](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-ii)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_triplet_value(nums: Vec<i32>) -> i64 {
        let n: usize = nums.len();
        let mut maximum_left: Vec<i64> = vec![-1; n+1];
        let mut maximum: i64 = 0;
        for index in 0..n {
            if nums[index] as i64 > maximum {
                maximum = nums[index] as i64;
            }

            maximum_left[index+1] = maximum;
        }

        let mut maximum_right: Vec<i64> = vec![-1; n+1];
        maximum = 0;
        for index in (1..n).rev() {
            if nums[index] as i64 > maximum {
                maximum = nums[index] as i64;
            }

            maximum_right[index-1] = maximum;
        }

        let mut result: i64 = 0;
        for index in 1..n-1 {
            if maximum_left[index] <= nums[index] as i64 {
                continue;
            }

            result = i64::max(result, (maximum_left[index]-nums[index] as i64) * maximum_right[index]);
        }

        return result
    }
}
```
