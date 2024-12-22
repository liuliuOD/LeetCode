![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2872. [Maximum Number Of K-Divisible Components](https://leetcode.com/problems/maximum-number-of-k-divisible-components)

### Solution :

Method 1 (DFS, Time Complexity: $O(M+N)$, Space Complexity: $O(M+N)$ (M: the number of the elements in `edges`, N: the value of `n`)) :
```rust
impl Solution {
    pub fn max_k_divisible_components(n: i32, edges: Vec<Vec<i32>>, values: Vec<i32>, k: i32) -> i32 {
        let mut adjust_list: Vec<Vec<usize>> = vec![vec![]; n as usize];
        for edge in edges {
            adjust_list[edge[0] as usize].push(edge[1] as usize);
            adjust_list[edge[1] as usize].push(edge[0] as usize);
        }

        let mut result: i32 = 0;
        Self::dfs(0, 0, &mut result, &adjust_list, &values, k);

        return result
    }

    fn dfs(current: usize, previous: usize, result: &mut i32, adjust_list: &Vec<Vec<usize>>, values: &Vec<i32>, k: i32) -> i32 {
        let mut sum: i32 = values[current] % k;
        for &next in &adjust_list[current] {
            if next == previous {
                continue;
            }

            sum = (sum+Self::dfs(next, current, result, adjust_list, values, k)) % k;
        }

        if sum == 0 {
            *result += 1;
        }
        return sum
    }
}
```
