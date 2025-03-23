![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1976. [Number Of Ways To Arrive At Destination](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/submissions/942449811/)

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

Method 2 (AI by Grok3, Binary Heap) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

const MOD: i64 = 1_000_000_007;
impl Solution {
    pub fn count_paths(n: i32, roads: Vec<Vec<i32>>) -> i32 {
        let n = n as usize;

        // Build adjacency list: (node, time)
        let mut graph: Vec<Vec<(usize, i64)>> = vec![vec![]; n];
        for road in roads {
            let u = road[0] as usize;
            let v = road[1] as usize;
            let time = road[2] as i64;
            graph[u].push((v, time));
            graph[v].push((u, time)); // Undirected graph
        }

        // Distance and ways arrays
        let mut dist: Vec<i64> = vec![i64::MAX; n];
        let mut ways: Vec<i64> = vec![0; n];
        dist[0] = 0;
        ways[0] = 1;

        // Priority queue: (distance, node)
        let mut pq = BinaryHeap::new();
        pq.push(Reverse((0, 0))); // Reverse for min-heap behavior

        while let Some(Reverse((d, u))) = pq.pop() {
            if d > dist[u] {
                continue; // Skip if we've found a shorter path already
            }

            for &(v, time) in &graph[u] {
                let new_dist = d + time;

                if new_dist < dist[v] {
                    // Found a shorter path
                    dist[v] = new_dist;
                    ways[v] = ways[u];
                    pq.push(Reverse((new_dist, v)));
                } else if new_dist == dist[v] {
                    // Found another path of equal length
                    ways[v] = (ways[v] + ways[u]) % MOD;
                }
            }
        }

        return ways[n - 1] as i32 // Return ways to reach destination
    }
}
```
