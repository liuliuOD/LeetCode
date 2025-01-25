![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2948. [Make Lexicographically Smallest Array By Swapping Elements](https://leetcode.com/problems/make-lexicographically-smallest-array-by-swapping-elements)

### Solution :

Method 1 (Graph, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn lexicographically_smallest_array(nums: Vec<i32>, limit: i32) -> Vec<i32> {
        let n: usize = nums.len();
        let mut nums_copy: Vec<i32> = nums.clone();
        nums_copy.sort();
        let mut graph: Vec<Vec<i32>> = Vec::from([vec![*nums_copy.last().unwrap(); 1]]);
        for index in (0..n-1).rev() {
            if (nums_copy[index]-nums_copy[index+1]).abs() <= limit {
                let m: usize = graph.len();
                graph[m-1].push(nums_copy[index]);
            } else {
                graph.push(vec![nums_copy[index]; 1]);
            }
        }

        let mut mapping: HashMap<i32, usize> = HashMap::new();
        for (index, group) in graph.iter().enumerate() {
            for &num in group {
                mapping.entry(num).or_insert(index);
            }
        }

        let mut result: Vec<i32> = Vec::new();
        for num in &nums {
            result.push(graph[*mapping.get(num).unwrap() as usize].pop().unwrap());
        }
        return result
    }
}
```
