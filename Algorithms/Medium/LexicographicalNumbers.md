![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 386. [Lexicographical Numbers](https://leetcode.com/problems/lexicographical-numbers)

### Solution :

Method 1 (Built-In Sorting, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn lexical_order(n: i32) -> Vec<i32> {
        let mut nums: Vec<String> = Vec::from((1..=n).map(|value| value.to_string()).collect::<Vec<String>>());
        nums.sort();

        return nums.iter()
            .map(|value| value.parse::<i32>().unwrap())
            .collect()
    }
}
```

Method 2 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(Log(N))$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn lexical_order(n: i32) -> Vec<i32> {
        let mut result: Vec<i32> = Vec::new();

        for value_current in 1..=9 {
            Self::dfs(value_current, &mut result, n);
        }

        return result
    }

    fn dfs(value_current: i32, result: &mut Vec<i32>, value_maximum: i32) {
        if value_current > value_maximum {
            return
        }
        result.push(value_current);

        for next_position in 0..=9 {
            Self::dfs(value_current*10+next_position, result, value_maximum);
        }
    }
}
```

Method 3 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(Log(N))$ (N: the value of `n`)) :
```rust
impl Solution {
    pub fn lexical_order(n: i32) -> Vec<i32> {
        let mut result: Vec<i32> = Vec::new();

        Self::dfs(0, &mut result, n);

        return result
    }

    fn dfs(value_current: i32, result: &mut Vec<i32>, value_maximum: i32) {
        for next_position in 0..=9 {
            let value_next: i32 = value_current*10 + next_position;

            if value_next > value_maximum {
                return
            }
            if value_next == 0 {
                continue;
            }

            result.push(value_next);

            Self::dfs(value_next, result, value_maximum);
        }
    }
}
```
