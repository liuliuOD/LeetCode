![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1497. [Check If Array Pairs Are Divisible By K](https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(K)$ (N: the number of the elements in `arr`, K: the value of `k`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn can_arrange(arr: Vec<i32>, k: i32) -> bool {
        let mut remainders: HashMap<i32, i32> = HashMap::new();
        for item in arr.iter() {
            remainders.entry(((item % k)+k) % k).and_modify(|amount| *amount += 1).or_insert(1);
        }

        for &remainder in remainders.keys() {
            if remainder == 0 {
                if remainders[&remainder] % 2 == 1 {
                    return false
                }
            } else {
                let target: i32 = k - (remainder % k);
                match remainders.get(&target) {
                    None => {
                        return false
                    },
                    Some(&amount) => {
                        if amount != remainders[&remainder] {
                            return false
                        }
                    }
                }
            }
        }

        return true
    }
}
```
