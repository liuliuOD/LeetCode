![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3219. [Minimum Cost For Cutting Cake II](https://leetcode.com/problems/minimum-cost-for-cutting-cake-ii)

### Solution :

Method 1 (Sorted + Greedy, Time Complexity: $O(M*Log(M)+N*Log(N))$, Space Complexity: $O(M+N)$ (M: number of the elements in `horizontal_cut`, N: number of the elements in `vertical_cut`)) :
```rust
impl Solution {
    pub fn minimum_cost(m: i32, n: i32, horizontal_cut: Vec<i32>, vertical_cut: Vec<i32>) -> i64 {
        let mut horizontal_sorted: Vec<(usize, &i32)> = horizontal_cut.iter().enumerate().collect();
        horizontal_sorted.sort_by_key(|&item| item.1);
        let mut vertical_sorted: Vec<(usize, &i32)> = vertical_cut.iter().enumerate().collect();
        vertical_sorted.sort_by_key(|&item| item.1);
        let mut current_m: i32 = 0;
        let mut current_n: i32 = 0;
        let mut result: i64 = 0;
        while horizontal_sorted.len() > 0 || vertical_sorted.len() > 0 {
            let mut num_h: i32 = 0;
            if horizontal_sorted.len() > 0 {
                num_h = *horizontal_sorted.last().unwrap().1;
            }
            let mut num_v: i32 = 0;
            if vertical_sorted.len() > 0 {
                num_v = *vertical_sorted.last().unwrap().1;
            }

            if num_h > num_v {
                horizontal_sorted.pop();
                result += (num_h*(current_n + 1)) as i64;
                current_m += 1;
            } else {
                vertical_sorted.pop();
                result += (num_v*(current_m + 1)) as i64;
                current_n += 1;
            }
        }

        return result
    }
}
```
