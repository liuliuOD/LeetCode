## [Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i)

### Solution :

Method 1 (Sliding Window + Big Integer) :
```rust
use std::cmp;
impl Solution {
    pub fn find_max_average(nums: Vec<i32>, k: i32) -> f64 {
        let offset = 10_i64.pow(5);
        let k = k as usize;
        let mut sum: i64 = 0;
        let mut result: i64 = i64::MIN;
        for i in 0..nums.len() {
            sum += nums[i] as i64 * offset;
            if i >= k - 1 {
                if i >= k {
                    sum -= nums[i-k] as i64 * offset;
                }
                result = cmp::max(result, sum / k as i64);
            }
        }
        result = cmp::max(result, sum / k as i64);

        result as f64 / offset as f64
    }
}
```

Method 2 (Sliding Window) :
```rust
use std::cmp;
impl Solution {
    pub fn find_max_average(nums: Vec<i32>, k: i32) -> f64 {
        let k = k as usize;
        let mut sum: i32 = nums[..k].iter().sum::<i32>();
        let mut result: i32 = sum;
        for i in k..nums.len() {
            sum += nums[i];
            sum -= nums[i-k];
            result = cmp::max(result, sum);
        }

        result as f64 / k as f64
    }
}
```
