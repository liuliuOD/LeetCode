![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2924. [Find Champion II](https://leetcode.com/problems/find-champion-ii)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(M)$, Space Complexity: $O(N)$ (M: the number of the elements in `edges`, N: the value of `n`)) :
```rust
impl Solution {
    pub fn find_champion(n: i32, edges: Vec<Vec<i32>>) -> i32 {
        let mut indegree: Vec<i32> = vec![0; n as usize];
        for edge in edges {
            indegree[edge[1] as usize] += 1;
        }

        let mut result: i32 = -1;
        for (index, amount) in indegree.into_iter().enumerate() {
            if amount == 0 {
                if result != -1 {
                    return -1
                }

                result = index as i32;
            }
        }

        return result
    }
}
```

Method 2 (Hash Set, Time Complexity: $O(M)$, Space Complexity: $O(N)$ (M: the number of the elements in `edges`, N: the value of `n`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn find_champion(n: i32, edges: Vec<Vec<i32>>) -> i32 {
        let mut visited: HashSet<i32> = HashSet::from_iter(edges.iter().map(|edge| edge[1]));

        return match visited.len() == (n as usize - 1) {
            false => -1,
            true => (0..n).filter(|num| !visited.contains(num)).collect::<Vec<i32>>()[0]
        }
    }
}
```
