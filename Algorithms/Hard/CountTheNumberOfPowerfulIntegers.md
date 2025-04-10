![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2999. [Count The Number Of Powerful Integers](https://leetcode.com/problems/count-the-number-of-powerful-integers)

### Solution :

Method 1 (AI by Grok3, ERROR: "Time Limit Exceeded", 267/932, Time Complexity: $O((F-S)/10^D*D)$, Space Complexity: $O(1)$ (F: the value of `finish`, S: the value of `start`, D: the amount of digit in `finish`)) :
```rust
impl Solution {
    pub fn number_of_powerful_int(start: i64, finish: i64, limit: i32, s: String) -> i64 {
        let suffix: i64 = s.parse().unwrap();
        let d = s.len() as i64; // Power of 10 for suffix shift
        let power = 10_i64.pow(d as u32);

        // Compute bounds for f
        let f_start = (start - suffix + power - 1) / power; // Ceiling division
        let f_finish = (finish - suffix) / power; // Floor division

        // If no valid f exists
        if f_finish < f_start || f_finish < 0 {
            return 0;
        }

        // Check each f in range and count valid ones
        let mut count = 0;
        let limit = limit as i64;

        for f in f_start..=f_finish {
            if Self::is_valid(f, limit) {
                let x = f * power + suffix;
                if x >= start && x <= finish {
                    count += 1;
                }
            }
        }

        return count
    }

    // Check if all digits of f are <= limit
    fn is_valid(mut f: i64, limit: i64) -> bool {
        if f == 0 {
            return true; // Special case: 0 has one digit, 0 <= limit
        }
        while f > 0 {
            if f % 10 > limit {
                return false
            }
            f /= 10;
        }
        return true
    }
}
```

Method 2 (AI by Grok3, Time Complexity: $O(Log(F))$, Space Complexity: $O(Log(F))$ (F: the value of `finish`)) :
```rust
impl Solution {
    pub fn number_of_powerful_int(start: i64, finish: i64, limit: i32, s: String) -> i64 {
        let count_up_to = |x: i64| -> i64 {
            if x < 0 {
                return 0
            }
            let x_str = x.to_string();
            let x_len = x_str.len();
            let s_len = s.len();
            let suffix: i64 = s.parse().unwrap();

            if x_len < s_len {
                return 0
            }

            let x_digits: Vec<i64> = x_str.chars()
                .map(|c| (c as u8 - b'0') as i64)
                .collect();
            let s_digits: Vec<i64> = s.chars()
                .map(|c| (c as u8 - b'0') as i64)
                .collect();

            let mut dp = vec![vec![-1; 2]; x_len + 1];

            fn digit_dp(pos: usize, tight: usize, x_digits: &Vec<i64>, s_digits: &Vec<i64>, limit: i64, dp: &mut Vec<Vec<i64>>) -> i64 {
                if pos == x_digits.len() {
                    return 1
                }
                if dp[pos][tight] != -1 {
                    return dp[pos][tight]
                }

                let max_digit = if tight == 1 { x_digits[pos] } else { 9 };
                let mut count = 0;

                if pos >= x_digits.len() - s_digits.len() {
                    let s_idx = pos - (x_digits.len() - s_digits.len());
                    let s_digit = s_digits[s_idx];
                    if s_digit > max_digit {
                        return 0
                    }
                    let new_tight = if tight == 1 && s_digit == x_digits[pos] { 1 } else { 0 };
                    count = digit_dp(pos + 1, new_tight, x_digits, s_digits, limit, dp);
                } else {
                    let digit_limit = max_digit.min(limit);
                    for d in (if pos == 0 { 1 } else { 0 })..=digit_limit {
                        let new_tight = if tight == 1 && d == x_digits[pos] { 1 } else { 0 };
                        count += digit_dp(pos + 1, new_tight, x_digits, s_digits, limit, dp);
                    }
                }

                dp[pos][tight] = count;

                return count
            }

            let mut total: i64 = 0;
            for len in s_len..x_len {
                let prefix_len = len - s_len;
                if prefix_len == 0 {
                    let num: i64 = s.parse().unwrap();
                    if num <= x {
                        total += 1;
                    }
                } else {
                    let first = limit as i64;
                    for d in 1..=first {
                        let count = (limit as i64 + 1).pow((prefix_len - 1) as u32);
                        total += count;
                    }
                }
            }

            total += digit_dp(0, 1, &x_digits, &s_digits, limit as i64, &mut dp);

            return total
        };

        let count_finish = count_up_to(finish);
        let count_start = count_up_to(start - 1);

        return count_finish - count_start
    }
}
```
