![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2551. [Put Marbles In Bags](https://leetcode.com/problems/put-marbles-in-bags)

### Solution :

Method 1 (AI by Grok3, Greedy, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `weights`)) :
```rust
impl Solution {
    pub fn put_marbles(weights: Vec<i32>, k: i32) -> i64 {
        let n = weights.len();
        if n == 1 || k == 1 {
            return 0; // Single bag or single marble, max = min
        }

        // Compute cut costs: weights[i] + weights[i+1]
        let mut cut_costs: Vec<i64> = (0..n-1)
            .map(|i| weights[i] as i64 + weights[i + 1] as i64)
            .collect();

        // Sort cut costs
        cut_costs.sort_unstable();

        // Min score: weights[0] + weights[n-1] + smallest (k-1) cuts
        // Max score: weights[0] + weights[n-1] + largest (k-1) cuts
        let k = k as usize;
        let min_sum: i64 = cut_costs[..k-1].iter().sum();
        let max_sum: i64 = cut_costs[n-k..].iter().sum();

        return max_sum - min_sum
    }
}
```
