![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2818. [Apply Operations To Maximize Score](https://leetcode.com/problems/apply-operations-to-maximize-score)

### Solution :

Method 1 (Time Complexity: $O()$, Space Complexity: $O()$ ()) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

impl Solution {
    const MOD: i64 = 1_000_000_007;

    pub fn maximum_score(nums: Vec<i32>, k: i32) -> i32 {
        let n = nums.len();
        let mut k = k as i64;

        // Step 1: Calculate prime factor counts (prime scores)
        let mut prime_scores = vec![0; n];
        for i in 0..n {
            let mut num = nums[i];
            let mut factor = 2;
            while factor * factor <= num {
                if num % factor == 0 {
                    prime_scores[i] += 1;
                    while num % factor == 0 {
                        num /= factor;
                    }
                }
                factor += 1;
            }
            if num >= 2 {
                prime_scores[i] += 1; // Remaining prime factor
            }
        }

        // Step 2: Compute next and previous dominant indices
        let mut next_dominant = vec![n as i32; n];
        let mut prev_dominant = vec![-1; n];
        let mut stack: Vec<usize> = Vec::new();

        for i in 0..n {
            while !stack.is_empty() && prime_scores[*stack.last().unwrap()] < prime_scores[i] {
                let top = stack.pop().unwrap();
                next_dominant[top] = i as i32;
            }
            if !stack.is_empty() {
                prev_dominant[i] = *stack.last().unwrap() as i32;
            }
            stack.push(i);
        }

        // Step 3: Calculate number of subarrays where each element is dominant
        let mut num_of_subarrays = vec![0i64; n];
        for i in 0..n {
            num_of_subarrays[i] = (next_dominant[i] - i as i32) as i64 * (i as i32 - prev_dominant[i]) as i64;
        }
        
        // Step 4: Priority queue for processing elements by value (max heap)
        let mut pq = BinaryHeap::new();
        for i in 0..n {
            pq.push((nums[i] as i64, i)); // (value, index)
        }

        let mut score = 1i64;

        // Step 5: Process elements greedily
        while k > 0 && !pq.is_empty() {
            let (num, idx) = pq.pop().unwrap();
            let operations = k.min(num_of_subarrays[idx]);
            score = (score * Self::power(num, operations)) % Self::MOD;
            k -= operations;
        }

        return score as i32
    }

    // Helper: Modular exponentiation
    fn power(mut base: i64, mut exp: i64) -> i64 {
        let mut res = 1;
        base %= Self::MOD;
        while exp > 0 {
            if exp % 2 == 1 {
                res = (res * base) % Self::MOD;
            }
            base = (base * base) % Self::MOD;
            exp /= 2;
        }

        return res
    }
}
````
