![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2275. [Largest Combination With Bitwise AND Greater Than Zero](https://leetcode.com/problems/largest-combination-with-bitwise-and-greater-than-zero)

### Solution :

Method 1 (DFS + Memoization, ERROR: "Time Limit Exceeded", 33/80, Time Complexity: $O(N*2^N)$, Space Complexity: $O(N*2^N)$ (N: the number of the elements in `candidates`)) :
```rust
use std::collections::HashMap;

const BASE: i32 = i32::MAX;
impl Solution {
    pub fn largest_combination(candidates: Vec<i32>) -> i32 {
        let mut memoization: HashMap<(usize, i32), i32> = HashMap::new();
        return Self::dfs(0, BASE, &mut memoization, &candidates)
    }

    fn dfs(index: usize, bitwise_and: i32, memoization: &mut HashMap<(usize, i32), i32>, candidates: &Vec<i32>) -> i32 {
        if index >= candidates.len() {
            return 0
        }

        let key: (usize, i32) = (index, bitwise_and);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let mut result: i32 = Self::dfs(index+1, bitwise_and, memoization, candidates);
        if bitwise_and & candidates[index] > 0 {
            result = i32::max(result, 1 + Self::dfs(index+1, bitwise_and & candidates[index], memoization, candidates));
        }
        memoization.entry(key).or_insert(result);
        return result
    }
}
```

Method 2 (Bitwise, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `candidates`)) :
```rust
impl Solution {
    pub fn largest_combination(candidates: Vec<i32>) -> i32 {
        let mut bitwise_counter: [i32; 24] = [0; 24];
        for candidate in candidates {
            for bit in 0..24 {
                if candidate & (1<<bit) > 0 {
                    bitwise_counter[bit] += 1;
                }
            }
        }

        return *bitwise_counter.iter().max().unwrap()
    }
}
```

Method 3 (Bitwise + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `candidates`)) :
```rust
impl Solution {
    pub fn largest_combination(candidates: Vec<i32>) -> i32 {
        let mut bitwise_counter: [i32; 24] = [0; 24];
        for candidate in candidates {
            for bit in 0..24 {
                let target: i32 = 1 << bit;
                if target > candidate {
                    break;
                }

                if candidate & target > 0 {
                    bitwise_counter[bit] += 1;
                }
            }
        }

        return bitwise_counter.into_iter().max().unwrap()
    }
}
```
