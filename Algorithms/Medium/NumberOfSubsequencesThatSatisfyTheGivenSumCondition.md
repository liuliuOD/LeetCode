![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Number Of Subsequences That Satisfy The Given Sum Condition](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition)

### Solution :

Method 1 (Two Pointer) :
```rust
impl Solution {
    pub fn num_subseq(mut nums: Vec<i32>, target: i32) -> i32 {
        let modulo: u64 = 10_u64.pow(9) + 7;
        nums.sort();

        let mut powers = vec![0; nums.len()];
        powers[0] = 1;
        for i in 1..nums.len() {
            powers[i] = (powers[i - 1] * 2) % modulo;
        }

        let mut i = 0;
        let mut j = nums.len() - 1;
        let mut result = 0;
        while i <= j && j < nums.len() {
            if nums[i] + nums[j] > target {
                j -= 1;
                continue;
            }

            result = (result + powers[j - i]) % modulo;
            i += 1;
        }

        result as i32
    }
}
```

Method 2 (ERROR: "Time Limit Exceeded") :
```rust
impl Solution {
    pub fn num_subseq(mut nums: Vec<i32>, target: i32) -> i32 {
        let modulo = 10_i32.pow(9) + 7;
        let mut candidates = vec![];
        nums.sort();

        for i in 0..nums.len() {
            for j in i..nums.len() {
                if nums[i] + nums[j] <= target {
                    candidates.push((i, j));
                }
            }
        }

        let mut powers = vec![0; nums.len()];
        powers[0] = 1;
        for i in 1..nums.len() {
          powers[i] = powers[i-1] * 2 % modulo;
        }

        let mut result = 0;
        while !candidates.is_empty() {
            let (num_min, num_max) = candidates.pop().unwrap();
            match num_max - num_min {
                0 | 1 => result += 1,
                value => result += powers[value - 1],
            }
            result %= modulo;
        }

        result
    }
}
```
