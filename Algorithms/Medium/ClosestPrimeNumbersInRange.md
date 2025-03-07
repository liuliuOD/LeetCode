![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2523. [Closest Prime Numbers In Range](https://leetcode.com/problems/closest-prime-numbers-in-range)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O((R-L)*$\sqrt{M}$)$, Space Complexity: $O(R-L)$ (L: the value of `left`, R: the value of `right`)) :
```rust
impl Solution {
    fn closest_primes(left: i32, right: i32) -> Vec<i32> {
        // Function to check if a number is prime
        fn is_prime(n: i32) -> bool {
            if n < 2 {
                return false;
            }

            for i in 2..=((n as f64).sqrt() as i32) {
                if n % i == 0 {
                    return false;
                }
            }

            return true
        }

        // Collect all prime numbers in the range
        let mut primes = Vec::new();
        for num in left..=right {
            if is_prime(num) {
                primes.push(num);
            }
        }

        // If less than 2 primes found, return [-1, -1]
        if primes.len() < 2 {
            return vec![-1, -1];
        }

        // Find the pair with minimum difference
        let mut min_diff = i32::MAX;
        let mut result = vec![-1, -1];
        for i in 0..primes.len()-1 {
            let diff = primes[i+1] - primes[i];
            if diff < min_diff {
                min_diff = diff;
                result = vec![primes[i], primes[i+1]];
            }
        }

        return result
    }
}
```

Method 2 (AI by Grok3, Time Complexity: $O(R*Log(Log(R))+R-L)$, Space Complexity: $O(R)$ (L: the value of `left`, R: the value of `right`)) :
```rust
impl Solution {
    pub fn closest_primes(left: i32, right: i32) -> Vec<i32> {
        let candidates: Vec<i32> = Self::sieve_of_eratosthenes(right as usize);
        let m: usize = candidates.len();
        let mut index: usize = 0;
        while index < m && candidates[index] < left {
            index += 1;
        }

        let mut result: Vec<i32> = vec![-1; 2];
        for index_current in index+1..m {
            if result[0] == -1 || (candidates[index_current]-candidates[index_current-1] < result[1]-result[0]) {
                result[0] = candidates[index_current-1];
                result[1] = candidates[index_current];
            }
        }

        return result
    }

    fn sieve_of_eratosthenes(n: usize) -> Vec<i32> {
        // Handle edge cases
        if n < 2 {
            return Vec::new();
        }

        // Initialize the sieve array: true means "potentially prime"
        let mut is_prime = vec![true; n + 1];
        is_prime[0] = false;
        is_prime[1] = false;

        // Sieve process
        for i in 2..=((n as f64).sqrt() as usize) {
            if is_prime[i] {
                // Mark multiples of i as non-prime
                for j in (i * i..=n).step_by(i) {
                    is_prime[j] = false;
                }
            }
        }

        // Collect primes into a vector
        return (2..=n)
            .filter(|&x| is_prime[x])
            .map(|x| x as i32)
            .collect()
    }
}
```
