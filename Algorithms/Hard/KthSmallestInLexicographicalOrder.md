![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 440. [K-th Smallest In Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order)

### Solution :

Method 1 (DFS, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$, ERROR: "Memory Limit Exceeded" (40/69)) :
```rust
impl Solution {
    pub fn find_kth_number(n: i32, k: i32) -> i32 {
        let mut result: Vec<i32> = Vec::new();

        Self::dfs(0, &mut result, n, k);

        return *result.last().unwrap()
    }

    fn dfs(value: i32, result: &mut Vec<i32>, n: i32, k: i32) {
        for position_next in 0..=9 {
            let value_next: i32 = value*10 + position_next;
            if value_next == 0 {
                continue;
            }

            if result.len() == k as usize {
                return
            }

            if value_next > n {
                return
            }
            result.push(value_next);

            Self::dfs(value_next, result, n, k);
        }
    }
}
```

Method 2 (DFS, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(Log(N))$, ERROR: "Time Limit Exceeded" (41/69)) :
```rust
impl Solution {
    pub fn find_kth_number(n: i32, k: i32) -> i32 {
        let mut amount: i32 = 0;
        let mut result: i64 = 0;

        Self::dfs(0, &mut result, &mut amount, n as i64, k);

        return result as i32
    }

    fn dfs(value: i64, result: &mut i64, amount: &mut i32, n: i64, k: i32) {
        for position_next in 0..=9 {
            let value_next: i64 = value*10 + position_next;
            if value_next == 0 {
                continue;
            }

            if *amount == k {
                return
            }

            if value_next > n {
                return
            }
            *amount += 1;
            *result = value_next;

            Self::dfs(value_next, result, amount, n, k);
        }
    }
}
```

Method 3 (Prefix Tree, Time Complexity: $O(Log(N)^2)$, Space Complexity: $O(Log(N))$) :
```rust
impl Solution {
    pub fn find_kth_number(n: i32, mut k: i32) -> i32 {
        let mut result: i64 = 1;
        k -= 1;
        while k > 0 {
            let amount: i32 = Self::amount_subtree(result, result+1, n as i64);

            if amount <= k {
                k -= amount;
                result += 1;
            } else {
                k -= 1;
                result *= 10;
            }
        }

        return result as i32
    }

    fn amount_subtree(mut value: i64, mut maximum: i64, n: i64) -> i32 {
        let mut result: i64 = 0;
        while value <= n {
            result += i64::min(n+1, maximum) - value;
            value *= 10;
            maximum *= 10;
        }

        return result as i32
    }
}
```
