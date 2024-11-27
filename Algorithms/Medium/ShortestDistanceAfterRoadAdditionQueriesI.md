![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3243. [Shortest Distance After Road Addition Queries I](https://leetcode.com/problems/shortest-distance-after-road-addition-queries-i)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(M*(M+N))$, Space Complexity: $O(M+N)$ (M: the number of the elements in `queries`, N: the value of `n`)) :
```rust
impl Solution {
    pub fn shortest_distance_after_queries(n: i32, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = n as usize;
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        for index in 1..n {
            graph[index-1].push(index);
        }

        let mut result: Vec<i32> = Vec::new();
        for query in queries {
            let u: usize = query[0] as usize;
            let v: usize = query[1] as usize;
            graph[u].push(v);
            result.push(Self::find_minimum_distance(&graph, n));
        }

        return result
    }

    fn find_minimum_distance(graph: &Vec<Vec<usize>>, n: usize) -> i32 {
        let mut dp: Vec<i32> = vec![0; n];
        for current in (0..n-1).rev() {
            let mut minimum_distance: i32 = n as i32;
            for &neighbor in graph[current].iter() {
                minimum_distance = i32::min(minimum_distance, dp[neighbor] + 1);
            }

            dp[current] = minimum_distance;
        }

        return dp[0]
    }
}
```
