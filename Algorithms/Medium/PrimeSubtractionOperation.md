![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2601. [Prime Subtraction Operation](https://leetcode.com/problems/prime-subtraction-operation)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn prime_sub_operation(nums: Vec<i32>) -> bool {
        let primes: Vec<i32> = Self::sieve_of_sundaram(1000);
        let mut num_previous: i32 = 0;
        for num in nums {
            let target: i32 = num - num_previous - 1;
            let difference: i32 = Self::binary_search(target, &primes);
            if difference <= target {
                num_previous = num - difference;
                continue;
            }

            if num_previous >= num {
                return false
            }
            num_previous = num;
        }

        return true
    }

    fn sieve_of_sundaram(num_maximum: i32) -> Vec<i32> {
        let k: usize = (num_maximum as usize-1) / 2;
        let mut primes: Vec<bool> = vec![true; k+1];
        for i in 1..((k as f64).sqrt() as usize) {
            let mut j: usize = i;
            while i+j+2*i*j <= k {
                primes[i+j+2*i*j] = false;
                j += 1;
            }
        }

        let mut result: Vec<i32> = Vec::from([2]);
        result.extend(
            primes.into_iter()
            .enumerate()
            .filter(|item| item.1 && item.0 > 0)
            .map(|item| item.0 as i32*2 + 1)
            .collect::<Vec<i32>>()
        );

        return result
    }

    fn binary_search(target: i32, candidates: &Vec<i32>) -> i32 {
        let mut left: usize = 0;
        let mut right: usize = candidates.len() - 1;
        while left <= right {
            let middle: usize = left + (right-left)/2;
            if candidates[middle] <= target {
                left = middle + 1;
            } else {
                if middle == 0 {
                    break;
                }

                right = middle - 1;
            }
        }

        return candidates[right]
    }
}
```
