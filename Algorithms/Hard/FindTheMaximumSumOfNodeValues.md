![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3068. [Find The Maximum Sum Of Node Values](https://leetcode.com/problems/find-the-maximum-sum-of-node-values)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_value_sum(nums: Vec<i32>, k: i32, edges: Vec<Vec<i32>>) -> i64 {
        let mut sum: i64 = 0;
        let mut count: i64 = 0;
        let mut positive_minimum: i64 = i64::MAX;
        let mut negative_maximum: i64 = i64::MIN;
        for num in nums {
            let operated_num: i32 = num ^ k;
            sum += num as i64;
            let net_change: i32 = operated_num - num;
            if net_change > 0 {
                positive_minimum = i64::min(positive_minimum, net_change as i64);
                sum += net_change as i64;
                count += 1;
                continue;
            }

            negative_maximum = i64::max(negative_maximum, net_change as i64);
        }

        if count % 2 == 0 {
            return sum
        }
        return i64::max(sum-positive_minimum, sum+negative_maximum)
    }
}
```
