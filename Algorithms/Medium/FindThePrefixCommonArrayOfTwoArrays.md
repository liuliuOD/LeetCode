![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2657. [Find The Prefix Common Array Of Two Arrays](https://leetcode.com/problems/find-the-prefix-common-array-of-two-arrays)

### Solution :

Method 1 (List, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `a`)) :
```rust
impl Solution {
    pub fn find_the_prefix_common_array(a: Vec<i32>, b: Vec<i32>) -> Vec<i32> {
        let n: usize = a.len();
        let mut visited: Vec<bool> = vec![false; n+1];
        let mut amount: i32 = 0;
        let mut result: Vec<i32> = vec![0; n];
        for index in 0..n {
            if visited[a[index] as usize] {
                amount += 1;
            }
            visited[a[index] as usize] = true;
            if visited[b[index] as usize] {
                amount += 1;
            }
            visited[b[index] as usize] = true;

            result[index] = amount;
        }

        return result
    }
}
```
