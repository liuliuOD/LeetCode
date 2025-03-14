![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2226. [Maximum Candies Allocated To K Children](https://leetcode.com/problems/maximum-candies-allocated-to-k-children)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(M))$, Space Complexity: $O(1)$ (M: the maximum element in `candies`, N: the number of elements in `candies`)) :
```rust
impl Solution {
    pub fn maximum_candies(candies: Vec<i32>, k: i64) -> i32 {
        if candies.iter().map(|num| *num as i64).sum::<i64>() < k {
            return 0
        }

        let mut left: i32 = 0;
        let mut right: i32 = *candies.iter().max().unwrap() + 1;
        while left < right {
            let middle: i32 = left + (right-left)/2;
            let mut amount: i64 = 0;
            for candy in candies.iter() {
                amount += (candy / middle) as i64;
            }

            if amount >= k {
                left = middle + 1;
            } else {
                right = middle;
            }
        }

        return left - 1
    }
}
```
