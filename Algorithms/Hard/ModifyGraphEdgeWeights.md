![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2699. [Modify Graph Edge Weights](https://leetcode.com/problems/modify-graph-edge-weights)

### Solution :

Method 1 (Dijkstra, Time Complexity: $O(E*V^2)$, Space Complexity: $O(V^2)$) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;

const MAXIMUM: i32 = 990_000_000;
impl Solution {
    pub fn modified_graph_edges(n: i32, mut edges: Vec<Vec<i32>>, source: i32, destination: i32, target: i32) -> Vec<Vec<i32>> {
        let shortest_distance: i32 = Self::dijkstra(n as usize, source as usize, destination as usize, &edges);

        if shortest_distance < target {
            return Vec::new()
        }

        let mut equal_to_target: bool = shortest_distance == target;
        for index in 0..edges.len() {
            if edges[index][2] != -1 {
                continue;
            }

            if equal_to_target {
                edges[index][2] = MAXIMUM;
                continue;
            }

            edges[index][2] = 1;
            let shortest_distance_next: i32 = Self::dijkstra(n as usize, source as usize, destination as usize, &edges);
            if shortest_distance_next <= target {
                equal_to_target = true;
                edges[index][2] += target - shortest_distance_next;
            }
        }

        return match equal_to_target {
            true => edges,
            false => Vec::new(),
        }
    }

    fn dijkstra(n: usize, source: usize, destination: usize, edges: &Vec<Vec<i32>>) -> i32 {
        let mut graph: Vec<Vec<i32>> = vec![vec![i32::MAX; n]; n];
        for edge in edges {
            let distance: i32 = edge[2];
            if distance == -1 {
                continue;
            }

            let a: usize = edge[0] as usize;
            let b: usize = edge[1] as usize;
            graph[a][b] = distance;
            graph[b][a] = distance;
        }

        let mut distances: Vec<i32> = vec![i32::MAX; n];
        let mut nodes: BinaryHeap<(Reverse<i32>, usize)> = BinaryHeap::from([(Reverse(0), source)]);
        while !nodes.is_empty() {
            let node: (Reverse<i32>, usize) = nodes.pop().unwrap();
            let Reverse(distance) = node.0;
            let index: usize = node.1;
            if distance >= distances[index] {
                continue;
            }
            distances[index] = distance;

            for index_next in 0..n {
                let mut distance_next: i32 = graph[index as usize][index_next];
                if distance_next != i32::MAX {
                    distance_next += distances[index];
                }
                if index == index_next || distance_next >= distances[index_next] {
                    continue;
                }

                nodes.push((Reverse(distance_next), index_next));
            }
        }

        return distances[destination]
    }
}
```
