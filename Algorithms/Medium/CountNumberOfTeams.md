![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1395. [Count Number Of Teams](https://leetcode.com/problems/count-number-of-teams)

### Solution :

Method 1 (Brute Force, Time Complexity: $(N^3)$, Space Complexity: $O(1)$ (N: numbers of the elements in `rating`)) :
```rust
impl Solution {
    pub fn num_teams(rating: Vec<i32>) -> i32 {
        let n: usize = rating.len();
        let mut result: i32 = 0;
        for index_first in 0..n-2 {
            let rate_first: i32 = rating[index_first];
            for index_second in index_first+1..n-1 {
                let rate_second: i32 = rating[index_second];
                for index_third in index_second+1..n {
                    let rate_third: i32 = rating[index_third];
                    if (rate_first > rate_second && rate_second > rate_third) || (rate_first < rate_second && rate_second < rate_third) {
                        result += 1;
                    }
                }
            }
        }

        return result
    }
}
```
