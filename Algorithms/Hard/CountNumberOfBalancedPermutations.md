![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3343. [Count Number Of Balanced Permutations](https://leetcode.com/problems/count-number-of-balanced-permutations)

### Solution :

Method 1 :
```rust
const MOD: i64 = 1_000_000_007;

impl Solution {
    pub fn count_balanced_permutations(num: String) -> i32 {
        let n = num.len();
        let mut cnt = [0; 10];
        let mut tot = 0;
        for ch in num.chars() {
            let d = ch.to_digit(10).unwrap() as usize;
            cnt[d] += 1;
            tot += d;
        }
        if tot % 2 != 0 {
            return 0;
        }

        let target = tot / 2;
        let max_odd = (n + 1) / 2;

        /* Pre-calculate combinations */
        let mut comb = vec![vec![0; max_odd + 1]; max_odd + 1];
        for i in 0..= max_odd {
            comb[i][i] = 1;
            comb[i][0] = 1;
            for j in 1..i {
                comb[i][j] = (comb[i-1][j] + comb[i - 1][j - 1]) % MOD;
            }
        }

        let mut psum = [0; 11];
        for i in (0..=9).rev() {
            psum[i] = psum[i + 1] + cnt[i];
        }

        let mut memo = vec![vec![vec![-1; max_odd+1]; target+1]; 10];

        fn dfs(
            pos: usize,
            curr: usize,
            odd_cnt: usize,
            cnt: &[usize],
            psum: &[usize],
            target: usize,
            max_odd: usize,
            comb: &Vec<Vec<i64>>,
            memo: &mut Vec<Vec<Vec<i64>>>
        ) -> i64 {
            /* If the remaining positions cannot be legally filled, or if the sum of the elements at the current odd positions is greater than the target value */
            if odd_cnt > max_odd || psum[pos] < odd_cnt || curr > target {
                return 0;
            }
            if pos > 9 {
                return if curr == target && odd_cnt == 0 { 1 } else { 0 };
            }
            if memo[pos][curr][odd_cnt] != -1 {
                return memo[pos][curr][odd_cnt];
            }

            /* Even-numbered positions remaining to be filled */
            let even_cnt = psum[pos] - odd_cnt;
            let start = (cnt[pos] as i32 - even_cnt as i32).max(0) as usize;
            let end = cnt[pos].min(odd_cnt);
            let mut res = 0;
            for i in start..= end {
                /* The current digit is filled with i positions at odd positions, and cnt[pos] - i positions at even positions */
                let ways = comb[odd_cnt][i] * comb[even_cnt][cnt[pos] - i] % MOD;
                res = (res + ways * dfs(pos + 1, curr + i * pos, odd_cnt - i, cnt, psum, target, max_odd, comb, memo) % MOD) % MOD;
            }
            memo[pos][curr][odd_cnt] = res;
            return res
        }

        return dfs(0, 0, max_odd, &cnt, &psum, target, max_odd, &comb, &mut memo) as i32
    }
}
```
