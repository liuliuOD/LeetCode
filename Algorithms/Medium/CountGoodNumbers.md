![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1922. [Count Good Numbers](https://leetcode.com/problems/count-good-numbers)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 69/166, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the value of `n`)) :
```rust
impl Solution {
    const MOD: i64 = 1_000_000_007;

    pub fn count_good_numbers(n: i64) -> i32 {
        let mut result: i64 = 5;
        let mut current_n: i64 = 1;
        while current_n < n {
            result = (result * match current_n%2 == 1 {
                true => 4,
                _ => 5,
            }) % Self::MOD;

            current_n += 1;
        }

        return result as i32
    }
}
```

Method 2 (Fast Exponentiation, Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$ (N: the value of `n`)) :
```rust
impl Solution {
    const MOD: i64 = 1_000_000_007;

    pub fn count_good_numbers(n: i64) -> i32 {
        return (Self::quick_multiply(5, (n+1)/2) * Self::quick_multiply(4, n/2) % Self::MOD) as i32
    }

    fn quick_multiply(x: i32, mut y: i64) -> i64 {
        let mut result: i64 = 1;
        let mut multiply: i64 = x as i64;
        while y > 0 {
            if y%2 == 1 {
                result = result * multiply % Self::MOD;
            }

            multiply = multiply * multiply % Self::MOD;
            y /= 2;
        }

        return result
    }
}
```
