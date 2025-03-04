![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1780. [Check If Number Is A Sum Of Powers Of Three](https://leetcode.com/problems/check-if-number-is-a-sum-of-powers-of-three)

### Solution :

Method 1 (DFS, Time Complexity: $O(2^N)$, Space Complexity: $O(Log(N))$ (N: the number of elements in `CANDIDATES`)) :
```rust
const CANDIDATES: [i32; 15] = [1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049, 177147, 531441, 1594323, 4782969];

impl Solution {
    pub fn check_powers_of_three(n: i32) -> bool {
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

Method 2 (DFS + Memoization, Time Complexity: $O(2^N)$, Space Complexity: $O(2^N)$ (N: the number of elements in `CANDIDATES`)) :
```rust
use std::collections::HashMap;

const CANDIDATES: [i32; 15] = [1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049, 177147, 531441, 1594323, 4782969];

impl Solution {
    pub fn check_powers_of_three(n: i32) -> bool {
        let mut memoization: HashMap<(i32, usize), bool> = HashMap::new();
        return Self::dfs(0, &mut memoization, n)
    }

    fn dfs(index: usize, memoization: &mut HashMap<(i32, usize), bool>, n: i32) -> bool {
        if n == 0 {
            return true
        }
        if index >= 15 {
            return false
        }

        let key: (i32, usize) = (n, index);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        return Self::dfs(index+1, memoization, n) || Self::dfs(index+1, memoization, n-CANDIDATES[index])
    }
}
```

Method 3 (Dynamic Programming, Time Complexity: $O(2^N)$, Space Complexity: $O(2^N)$ (N: the number of elements in `CANDIDATES`)) :
```rust
use std::collections::HashSet;

const CANDIDATES: [i32; 15] = [1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049, 177147, 531441, 1594323, 4782969];

impl Solution {
    pub fn check_powers_of_three(n: i32) -> bool {
        let mut dp: HashSet<i32> = HashSet::new();
        for index in 0..15 {
            let mut temp: HashSet<i32> = HashSet::from([CANDIDATES[index]]);
            for &num in &dp {
                if num == n || num+CANDIDATES[index] == n {
                    return true
                }

                temp.insert(num+CANDIDATES[index]);
            }

            for num in temp {
                dp.insert(num);
            }
        }

        return false
    }
}
```
