![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 873. [Length Of Longest Fibonacci Subsequence](https://leetcode.com/problems/length-of-longest-fibonacci-subsequence)

### Solution :

Method 1 (Brute Force + Hash Set, Time Complexity: $O(N^2*Log(M))$, Space Complexity: $O(N)$ (M: the maximum element in `arr`, N: the number of elements in `arr`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn len_longest_fib_subseq(arr: Vec<i32>) -> i32 {
        let n: usize = arr.len();
        let mut mapper: HashSet<i32> = HashSet::from_iter(arr.clone());
        let mut result: i32 = 0;
        for index_start in 0..n {
            for index_next in index_start+1..n {
                let mut previous: i32 = arr[index_next];
                let mut current: i32 = arr[index_start] + arr[index_next];
                let mut amount: i32 = 2;
                while mapper.contains(&current) {
                    amount += 1;
                    let temp: i32 = previous + current;
                    previous = current;
                    current = temp;
                }

                if amount > 2 {
                    result = i32::max(result, amount);
                }
            }
        }

        return result
    }
}
```
