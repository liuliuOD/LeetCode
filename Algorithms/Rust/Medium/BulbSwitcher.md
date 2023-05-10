![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Bulb Switcher](https://leetcode.com/problems/bulb-switcher)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn bulb_switch(n: i32) -> i32 {
        f64::sqrt(n as f64) as _
    }
}
```

Method 2 (Brute Force, ERROR: "Time Limit Exceeded" when n = 99999999):
```rust
impl Solution {
    pub fn bulb_switch(n: i32) -> i32 {
        match n {
            0 | 1 => n,
            n => {
                let mut bulbs = vec![true; n as usize];
                for i in 2..n+1 {
                    let mut j = i - 1;
                    while j < n {
                        bulbs[j as usize] = !bulbs[j as usize];
                        j += i;
                    }
                }

                bulbs.iter().filter(|&&x| x).count() as _
            }
        }
    }
}
```

Method 3 (Brute Force, ERROR: "Time Limit Exceeded" when n = 99999999) :
```rust
impl Solution {
    pub fn bulb_switch(n: i32) -> i32 {
        let mut bulbs = vec![true; n as usize];

        for mut i in 2..n+1{
            let mut j = i - 1;
            loop {
                if j >= n {
                    break;
                }

                bulbs[j as usize] = !bulbs[j as usize];

                j += i;
            }
        }

        bulbs.iter().filter(|&&x| x).count() as _
    }
}
```
