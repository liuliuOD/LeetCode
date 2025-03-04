![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1780. [Check If Number Is A Sum Of Powers Of Three](https://leetcode.com/problems/check-if-number-is-a-sum-of-powers-of-three)

### Solution :

Method 1 (DFS, Time Complexity: $O(2^N)$, Space Complexity: $O(Log(N))$ (N: the number of elements in `CANDIDATES`)) :
```rust
const CANDIDATES: [i32; 15] = [1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049, 177147, 531441, 1594323, 4782969];

impl Solution {
    pub fn check_powers_of_three(n: i32) -> bool {
        let mut index: usize = 14;
        return Self::dfs(0, n)
    }

    fn dfs(index: usize, n: i32) -> bool {
        if n == 0 {
            return true
        }
        if index >= 15 {
            return false
        }

        return Self::dfs(index+1, n) || Self::dfs(index+1, n-CANDIDATES[index])
    }
}
```
