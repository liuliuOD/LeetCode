![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1140. [Stone Game II](https://leetcode.com/problems/stone-game-ii)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N^3)$, Space Complexity: $O(N^2)$ (N: the number of the elements in `piles`)) :
```rust
impl Solution {
    pub fn stone_game_ii(piles: Vec<i32>) -> i32 {
        let n: usize = piles.len();
        let mut suffix_sum: Vec<i32> = vec![0; n];
        suffix_sum[n-1] = piles[n-1];
        for index in (0..n-1).rev() {
            suffix_sum[index] = suffix_sum[index+1] + piles[index];
        }
        let mut memoization: Vec<Vec<i32>> = vec![vec![-1; n]; n];
        return Self::dfs(0, 1, &mut memoization, &piles, &suffix_sum)
    }

    fn dfs(index: usize, M: i32, memoization: &mut Vec<Vec<i32>>, piles: &Vec<i32>, suffix_sum: &Vec<i32>) -> i32 {
        let n: usize = piles.len();
        if index+2*M as usize >= n {
            return suffix_sum[index]
        }

        if memoization[index][M as usize] >= 0 {
            return memoization[index][M as usize]
        }

        let mut opponent_stones: i32 = i32::MAX;
        for amount in 1..=2*M as usize {
            opponent_stones = i32::min(opponent_stones, Self::dfs(index+amount, i32::max(M, amount as i32), memoization, piles, suffix_sum));
        }

        memoization[index][M as usize] = suffix_sum[index] - opponent_stones;
        return memoization[index][M as usize]
    }
}
```
