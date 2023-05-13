![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2466. [Count Ways To Build Good Strings](https://leetcode.com/problems/count-ways-to-build-good-strings)

### Solution :

Method 1 (DP without memoization, ERROR: "Time Limit Exceeded") :
```rust
impl Solution {
    pub fn count_good_strings(low: i32, high: i32, zero: i32, one: i32) -> i32 {
        let mut result = 0;
        for n in low..high+1 {
            result += Self::dynamic_programming(n, zero, one);
        }

        result
    }

    fn dynamic_programming(n: i32, zero: i32, one: i32) -> i32 {
        if n == 0 {
            return 1
        } else if n < 0 || (n < zero && n < one) {
            return 0
        }

        Self::dynamic_programming(n-zero, zero, one) + Self::dynamic_programming(n-one, zero, one)
    }
}
```

Method 2 (HashMap DP with memoization and Top Down, much slower, time used: 50ms) :
```rust
use std::collections::HashMap;
const MODULO: i32 = 10_i32.pow(9) + 7;
impl Solution {
    pub fn count_good_strings(low: i32, high: i32, zero: i32, one: i32) -> i32 {
        let mut hm: HashMap<i32, i32> = HashMap::new();
        let mut result = 0;
        for n in low..high+1 {
            result = (result + Self::dynamic_programming(n, zero, one, &mut hm) % MODULO) % MODULO;
        }

        result
    }

    fn dynamic_programming(n: i32, zero: i32, one: i32, hm: &mut HashMap<i32, i32>) -> i32 {
        if n == 0 {
            return 1
        } else if n < 0 || (n < zero && n < one) {
            return 0
        }

        if hm.contains_key(&n) {
            return *hm.get(&n).unwrap()
        }

        let temp = (Self::dynamic_programming(n-zero, zero, one, hm) % MODULO + Self::dynamic_programming(n-one, zero, one, hm) % MODULO) % MODULO;
        hm.insert(n, temp);
        temp
    }
}
```

Method 3 (Vector DP with memoization and Top Down, much faster, time used: 7ms) :
```rust
const MODULO: i32 = 10_i32.pow(9) + 7;
impl Solution {
    pub fn count_good_strings(low: i32, high: i32, zero: i32, one: i32) -> i32 {
        let mut hm: Vec<i32> = vec![-1; high as usize + 1];
        hm[0] = 1;
        let mut result = 0;
        for n in low..high+1 {
            result = (result + Self::dynamic_programming(n, zero, one, &mut hm) % MODULO) % MODULO;
        }

        result
    }

    fn dynamic_programming(n: i32, zero: i32, one: i32, hm: &mut Vec<i32>) -> i32 {
        if n == 0 {
            return 1
        } else if n < 0 || (n < zero && n < one) {
            return 0
        }

        if hm[n as usize] >= 0 {
            return hm[n as usize]
        }

        let temp = (Self::dynamic_programming(n-zero, zero, one, hm) % MODULO + Self::dynamic_programming(n-one, zero, one, hm) % MODULO) % MODULO;
        hm[n as usize] = temp;
        temp
    }
}
```

Method 4 (DP with memoization and Bottom Up, fastest, time used: 2ms) :
```rust
const MODULO: i32 = 10_i32.pow(9) + 7;
impl Solution {
    pub fn count_good_strings(low: i32, high: i32, zero: i32, one: i32) -> i32 {
        let (low, high) = (low as usize, high as usize);
        let (zero, one) = (zero as usize, one as usize);
        let mut hm: Vec<i32> = vec![0; high+1];
        hm[0] = 1;
        let mut result = 0;
        for n in 1..high+1 {
            if n >=zero {
                hm[n] += hm[n-zero];
            }
            if n >= one {
                hm[n] += hm[n-one];
            }
            hm[n] %= MODULO;

            if n >= low {
                result += hm[n];
                result %= MODULO;
            }
        }

        result
    }
}
```
