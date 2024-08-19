![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 650. [2 Keys Keyboard](https://leetcode.com/problems/2-keys-keyboard)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the value of `n`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn min_steps(n: i32) -> i32 {
        let mut memoization: HashMap<String, i32> = HashMap::new();
        return Self::dfs(0, 1, false, &mut memoization, n)
    }

    fn dfs(amount_copy: i32, amount_screen: i32, copied: bool,memoization: &mut HashMap<String, i32>, n: i32) -> i32 {
        let key: String = format!("{}-{}-{}", copied, amount_copy, amount_screen);
        if memoization.contains_key(&key) {
            return memoization[&key]
        }

        if amount_screen == n {
            return 0
        }
        else if amount_screen > n {
            return i32::MAX
        }

        let mut copy: i32 = i32::MAX;
        if !copied {
            copy = Self::dfs(amount_screen, amount_screen, true, memoization, n);
            if copy != i32::MAX {
                copy += 1;
            }
        }
        let mut paste: i32 = i32::MAX;
        if amount_copy > 0 {
            paste = Self::dfs(amount_copy, amount_screen+amount_copy, false, memoization, n);
            if paste != i32::MAX {
                paste += 1;
            }
        }
        memoization.insert(key.clone(), i32::min(copy, paste));
        return memoization[&key]
    }
}
```
