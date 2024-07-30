![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1653. [Minimum Deletions To Make String Balanced](https://leetcode.com/problems/minimum-deletions-to-make-string-balanced)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $(N)$, Space Complexity: $O(N)$ (N: length of `s`)) :
```rust
struct Counter {
    a: usize,
    b: usize
}

impl Solution {
    pub fn minimum_deletions(s: String) -> i32 {
        let mut counter: Vec<Counter> = Vec::from([Counter{a: 0, b: 0}]);
        for ch in s.bytes() {
            let last: &Counter = counter.last().unwrap();
            if ch == b'a' {
                counter.push(Counter{a: last.a+1, b: last.b});
            } else if ch == b'b' {
                counter.push(Counter{a: last.a, b: last.b+1});
            }
        }

        let mut result: i32 = i32::MAX;
        for instance in &counter {
            result = result.min((instance.b+counter.last().unwrap().a-instance.a) as i32);
        }

        return result
    }
}
```

Method 2 (Time Complexity: $(N)$, Space Complexity: $O(1)$ (N: length of `s`)) :
```rust
impl Solution {
    pub fn minimum_deletions(s: String) -> i32 {
        if s.len() <= 1 {
            return 0
        }

        let mut amount_a: usize = 0;
        let mut amount_b: usize = 0;
        for ch in s.bytes() {
            if ch == b'a' {
                amount_a += 1;
            } else if ch == b'b' {
                amount_b += 1;
            }
        }

        let mut result: i32 = i32::MAX;
        let mut amount_a_current: usize = 0;
        let mut amount_b_current: usize = 0;
        for ch in s.bytes() {
            if ch == b'a' {
                amount_a_current += 1;
            }

            result = result.min((amount_b_current+amount_a-amount_a_current) as i32);

            if ch == b'b' {
                amount_b_current += 1;
            }
        }

        return result
    }
}
```
