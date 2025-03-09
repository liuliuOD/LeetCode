![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3208. [Alternating Groups II](https://leetcode.com/problems/alternating-groups-ii)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N+K)$, Space Complexity: $O(N)$ (N: the number of elements in `colors`, K: the value of `k`)) :
```rust
impl Solution {
    pub fn number_of_alternating_groups(mut colors: Vec<i32>, k: i32) -> i32 {
        let n: usize = colors.len();
        /* Option 1 */
        colors.append(&mut colors.clone());
        /* Option 2
        colors.extend_from_slice(&colors[0..k as usize].to_vec());
        */
        let mut amount_alternating: usize = 1;
        let mut index_start: usize = 0;
        let mut index_current: usize = 1;
        let mut result: i32 = 0;
        while index_current < n-1+k as usize {
            amount_alternating += 1;

            if colors[index_current] == colors[index_current-1] {
                amount_alternating -= (index_current - index_start);
                index_start = index_current;
            }

            if amount_alternating as i32 >= k {
                result += 1;
            }

            index_current += 1;
        }

        return result
    }
}
```
