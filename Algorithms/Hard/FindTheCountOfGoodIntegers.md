![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3272. [Find The Count of Good Integers](https://leetcode.com/problems/find-the-count-of-good-integers)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N)*10^M)$, Space Complexity: $O(N*10^M)$ (N: the value of `n`, M: (N+1)/2)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn count_good_integers(n: i32, k: i32) -> i64 {
        let mut dict: HashSet<String> = HashSet::new();
        let base = 10i32.pow(((n - 1) / 2) as u32);
        let skip = (n & 1) as usize;
        /* Enumerate the number of palindrome numbers of n digits */
        for i in base..base * 10 {
            let s = i.to_string();
            let rev: String = s.chars().rev().skip(skip).collect();
            let combined = format!("{}{}", s, rev);
            let palindromicInteger: i64 = combined.parse().unwrap();
            /* If the current palindrome number is a k-palindromic integer */
            if palindromicInteger % (k as i64) == 0 {
                let mut sorted_chars: Vec<char> = combined.chars().collect();
                sorted_chars.sort();
                dict.insert(sorted_chars.into_iter().collect());
            }
        }

        let mut factorial = vec![1i64; (n + 1) as usize];
        for i in 1..=n as usize {
            factorial[i] = factorial[i - 1] * (i as i64);
        }

        let mut ans = 0i64;
        for s in dict {
            let mut cnt = vec![0; 10];
            for c in s.chars() {
                cnt[c.to_digit(10).unwrap() as usize] += 1;
            }
            /* Calculate permutations and combinations */
            let mut tot = (n as i64 - cnt[0] as i64) * factorial[(n - 1) as usize];
            for &x in cnt.iter() {
                tot /= factorial[x];
            }
            ans += tot;
        }

        return ans
    }
}
```
