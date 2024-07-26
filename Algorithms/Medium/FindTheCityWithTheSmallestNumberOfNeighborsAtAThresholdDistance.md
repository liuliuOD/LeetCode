![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1334. [Find The City With The Smallest Number Of Neighbors At A Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance)

### Solution :

Method 1 (Floyd Warshall, Time Complexity: $(N^3)$, Space Complexity: $O(N^2)$) :
```rust
impl Solution {
    pub fn find_the_city(n: i32, edges: Vec<Vec<i32>>, distance_threshold: i32) -> i32 {
        let n: usize = n as usize;
        /* Option 1 */
        let mut graph: Vec<Vec<i32>> = Vec::with_capacity(n);
        for _ in 0..n {
            let mut item: Vec<i32> = Vec::with_capacity(n);
            for _ in 0..n {
                item.push(i32::MAX);
            }

            graph.push(item);
        }
        /* Option 2

        let mut graph: Vec<Vec<i32>> = vec![vec![i32::MAX; n]; n];
        */

        for edge in edges {
            let from: usize = edge[0] as usize;
            let to: usize = edge[1] as usize;
            let weight = edge[2];
            graph[from][to] = i32::min(graph[from][to], weight);
            graph[to][from] = i32::min(graph[to][from], weight);
        }

        Self::floyd_warshall(&mut graph);

        /* Option 1 */
        let mut mapping: Vec<Vec<usize>> = Vec::with_capacity(n);
        for _ in 0..n {
            mapping.push(Vec::new());
        }
        /* Option 2

        let mut mapping: Vec<Vec<usize>> = vec![Vec::new(); n];
        */

        let mut minimum_length: usize = usize::MAX;
        for index_i in 0..n {
            for index_j in 0..n {
                if index_i == index_j {
                    continue
                }

                if graph[index_i][index_j] <= distance_threshold {
                    mapping[index_i].push(index_j);
                }
            }
            minimum_length = minimum_length.min(mapping[index_i].len());
        }

        return (0..n).rev().find(|&index| mapping[index].len() == minimum_length).unwrap() as i32
    }

    fn floyd_warshall(graph: &mut Vec<Vec<i32>>) {
        let n: usize = graph.len();
        for index_k in 0..n {
            for index_i in 0..n {
                for index_j in 0..n {
                    if graph[index_i][index_k] == i32::MAX || graph[index_k][index_j] == i32::MAX {
                        continue
                    }

                    graph[index_i][index_j] = i32::min(graph[index_i][index_j], graph[index_i][index_k] + graph[index_k][index_j]);
                }
            }
        }
    }
}
```
