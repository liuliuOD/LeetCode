![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3259. [Maximum Energy Boost From Two Drinks](https://leetcode.com/problems/maximum-energy-boost-from-two-drinks)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `energy_drink_a`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn max_energy_boost(energy_drink_a: Vec<i32>, energy_drink_b: Vec<i32>) -> i64 {
        let mut memoization: HashMap<String, i64> = HashMap::new();
        return i64::max(energy_drink_a[0] as i64+Self::dfs(1, 0, &mut memoization, &energy_drink_a, &energy_drink_b), energy_drink_b[0] as i64+Self::dfs(1, 1, &mut memoization, &energy_drink_a, &energy_drink_b))
    }

    fn dfs(index: usize, previous: usize, memoization: &mut HashMap<String, i64>, energy_a: &Vec<i32>, energy_b: &Vec<i32>) -> i64 {
        let n: usize = energy_a.len();
        if index >= n {
            return 0
        }

        let mut current: i64 = energy_a[index] as i64;
        if previous == 1 {
            current = energy_b[index] as i64;
        }

        let key: String = format!("{}-{}", previous, index);
        if memoization.contains_key(&key) {
            return memoization[&key]
        }

        let value_change: i64 = Self::dfs(index+1, (previous+1)%2, memoization, energy_a, energy_b);
        let value_keep: i64 = current + Self::dfs(index+1, previous, memoization, energy_a, energy_b);
        memoization.insert(key.clone(), i64::max(value_change, value_keep));

        return memoization[&key]
    }
}
```

Method 2 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `energy_drink_a`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn max_energy_boost(energy_drink_a: Vec<i32>, energy_drink_b: Vec<i32>) -> i64 {
        let mut memoization: [HashMap<usize, i64>; 2] = [HashMap::new(), HashMap::new()];
        return i64::max(energy_drink_a[0] as i64+Self::dfs(1, 0, &mut memoization, &energy_drink_a, &energy_drink_b), energy_drink_b[0] as i64+Self::dfs(1, 1, &mut memoization, &energy_drink_a, &energy_drink_b))
    }

    fn dfs(index: usize, previous: usize, memoization: &mut [HashMap<usize, i64>; 2], energy_a: &Vec<i32>, energy_b: &Vec<i32>) -> i64 {
        let n: usize = energy_a.len();
        if index >= n {
            return 0
        }

        let mut current: i64 = energy_a[index] as i64;
        if previous == 1 {
            current = energy_b[index] as i64;
        }

        if memoization[previous].contains_key(&index) {
            return memoization[previous][&index]
        }

        let value_change: i64 = Self::dfs(index+1, (previous+1)%2, memoization, energy_a, energy_b);
        let value_keep: i64 = current + Self::dfs(index+1, previous, memoization, energy_a, energy_b);
        memoization[previous].insert(index, i64::max(value_change, value_keep));

        return memoization[previous][&index]
    }
}
```
