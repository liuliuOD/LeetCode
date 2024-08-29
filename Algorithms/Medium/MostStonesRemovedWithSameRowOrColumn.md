![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 947. [Most Stones Removed With Same Row Or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column)

### Solution :

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `stones`)) :
```rust
use std::collections::{HashMap, HashSet};

impl Solution {
    pub fn remove_stones(stones: Vec<Vec<i32>>) -> i32 {
        let n: usize = stones.len();
        let mut mapping_x: HashMap<usize, Vec<usize>> = HashMap::new();
        let mut mapping_y: HashMap<usize, Vec<usize>> = HashMap::new();
        for index in 0..n {
            let stone: &Vec<i32> = &stones[index];
            mapping_x.entry(stone[0] as usize).and_modify(|group| group.push(index)).or_insert(Vec::from([index]));
            mapping_y.entry(stone[1] as usize).and_modify(|group| group.push(index)).or_insert(Vec::from([index]));
        }

        return n as i32 - Self::find_the_number_of_groups(&mapping_x, &mapping_y, &stones)
    }

    fn find_the_number_of_groups(mapping_x: &HashMap<usize, Vec<usize>>, mapping_y: &HashMap<usize, Vec<usize>>, stones: &Vec<Vec<i32>>) -> i32 {
        let n: usize = stones.len();
        let mut visited: HashSet<usize> = HashSet::new();
        let mut result: i32 = 0;
        for index in 0..n {
            if visited.contains(&index) {
                continue;
            }
            result += 1;

            Self::dfs(index, &mut visited, mapping_x, mapping_y, stones);
        }

        return result
    }

    fn dfs(index: usize, visited: &mut HashSet<usize>, mapping_x: &HashMap<usize, Vec<usize>>, mapping_y: &HashMap<usize, Vec<usize>>, stones: &Vec<Vec<i32>>) {
        if visited.contains(&index) {
            return
        }
        visited.insert(index);

        for &index_neighbor in mapping_x[&(stones[index][0] as usize)].iter() {
            Self::dfs(index_neighbor, visited, mapping_x, mapping_y, stones);
        }
        for &index_neighbor in mapping_y[&(stones[index][1] as usize)].iter() {
            Self::dfs(index_neighbor, visited, mapping_x, mapping_y, stones);
        }
    }
}
```
