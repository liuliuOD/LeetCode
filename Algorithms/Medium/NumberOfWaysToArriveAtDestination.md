![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Number Of Ways To Arrive At Destination](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/submissions/942449811/)

### Solution :

Method 1 (Dijkstra) :
```rust
use std::cmp::Ordering;
use std::collections::BinaryHeap;
impl Solution {
    pub fn count_paths(n: i32, roads: Vec<Vec<i32>>) -> i32 {
        let mut distances = vec![i64::MAX; n as usize];
        let mut results = vec![0; n as usize];
        let mut graph = vec![vec![]; n as usize];

        // build the graph
        for edge in roads {
            graph[edge[0] as usize].push((edge[1] as usize, edge[2]));
            graph[edge[1] as usize].push((edge[0] as usize, edge[2]));
        }

        distances[0] = 0;
        results[0] = 1;
        let mut heap = BinaryHeap::from([(0, 0)]);
        while heap.len() > 0 {
            if let Some((mut time, point)) = heap.pop() {
                time = i64::abs(time);
                for target in graph[point].iter() {
                    let point_target = target.0;
                    let time_from_current_to_target = target.1 as i64;
                    let time_to_target = time + time_from_current_to_target;

                    match time_to_target.cmp(&distances[point_target]) {
                        Ordering::Equal => {
                            results[point_target] += results[point];
                            results[point_target] %= (10_i32.pow(9) + 7); // prevent overflow
                        },
                        Ordering::Less => {
                            results[point_target] = results[point];
                            distances[point_target] = time_to_target;
                            heap.push((-time_to_target, point_target));
                        },
                        _ => (),
                    }
                }
            }
        }

        results[(n - 1) as usize] % (10_i32.pow(9) + 7)
    }
}
```
