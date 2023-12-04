![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2952. [Minimum Number Of Coins To Be Added](https://leetcode.com/problems/minimum-number-of-coins-to-be-added)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn minimum_added_coins(mut coins: Vec<i32>, target: i32) -> i32 {
        coins.sort();
        let n: usize = coins.len();
        let mut miss: i32 = 1;
        let mut index: usize = 0;
        let mut result: i32 = 0;
        while miss <= target {
            if index < n && coins[index] <= miss {
                miss += coins[index];
                index += 1;
            } else {
                miss += miss;
                result += 1;
            }
        }

        return result
    }
}
```
