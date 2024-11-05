![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2914. [Minimum Number Of Changes To Make Binary String Beautiful](https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful)

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded", 504/577, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let n: usize = s.len();
        let s_char: Vec<u8> = s.as_bytes().to_vec();
        let mut prefix_sum_one: Vec<i32> = vec![0; n+1];
        for index in 0..n {
            prefix_sum_one[index+1] = prefix_sum_one[index];
            if s_char[index] == b'1' {
                prefix_sum_one[index+1] += 1;
            }
        }

        return i32::min(
            Self::dfs(0, b'0', &s_char, &prefix_sum_one),
            Self::dfs(0, b'1', &s_char, &prefix_sum_one),
        )
    }

    fn dfs(index: usize, element: u8, s_char: &Vec<u8>, prefix_sum_one: &Vec<i32>) -> i32 {
        if index >= s_char.len()-1 {
            return 0
        }

        let mut result: i32 = match element {
            b'0' => prefix_sum_one[index+2] - prefix_sum_one[index],
            b'1' | _ => 2 - (prefix_sum_one[index+2] - prefix_sum_one[index]),
        };

        return result + i32::min(
            Self::dfs(index+2, b'0', s_char, prefix_sum_one),
            Self::dfs(index+2, b'1', s_char, prefix_sum_one),
        )
    }
}
```

Method 2 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn min_changes(s: String) -> i32 {
        let n: usize = s.len();
        let s_char: Vec<u8> = s.as_bytes().to_vec();
        let mut prefix_sum_one: Vec<i32> = vec![0; n+1];
        for index in 0..n {
            prefix_sum_one[index+1] = prefix_sum_one[index];
            if s_char[index] == b'1' {
                prefix_sum_one[index+1] += 1;
            }
        }

        let mut memoization: HashMap<(usize, u8), i32> = HashMap::new();
        return i32::min(
            Self::dfs(0, b'0', &mut memoization, &s_char, &prefix_sum_one),
            Self::dfs(0, b'1', &mut memoization, &s_char, &prefix_sum_one),
        )
    }

    fn dfs(index: usize, element: u8, memoization: &mut HashMap<(usize, u8), i32>, s_char: &Vec<u8>, prefix_sum_one: &Vec<i32>) -> i32 {
        if index >= s_char.len()-1 {
            return 0
        }

        let key: (usize, u8) = (index, element);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let mut result: i32 = match element {
            b'0' => prefix_sum_one[index+2] - prefix_sum_one[index],
            b'1' | _ => 2 - (prefix_sum_one[index+2] - prefix_sum_one[index]),
        };

        result += i32::min(
            Self::dfs(index+2, b'0', memoization, s_char, prefix_sum_one),
            Self::dfs(index+2, b'1', memoization, s_char, prefix_sum_one),
        );

        memoization.entry(key).or_insert(result);
        return result
    }
}
```
