![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3203. [Find Minimum Diameter After Merging Two Trees](https://leetcode.com/problems/find-minimum-diameter-after-merging-two-trees)

### Solution :

Method 1 (BFS + Hash Set, Time Complexity: $O(M+N)$, Space Complexity: $O(M+N)$ (M: the number of the elements in `edges1`, N: the number of the elements in `edges2`)) :
```rust
use std::collections::{HashSet, VecDeque};

impl Solution {
    pub fn minimum_diameter_after_merge(edges1: Vec<Vec<i32>>, edges2: Vec<Vec<i32>>) -> i32 {
        let adjust_list1: Vec<Vec<usize>> = Self::get_adjust_list(&edges1);
        let adjust_list2: Vec<Vec<usize>> = Self::get_adjust_list(&edges2);

        let maximum_diameter1: i32 = Self::find_maximum_diameter(&adjust_list1);
        let maximum_diameter2: i32 = Self::find_maximum_diameter(&adjust_list2);

        return [maximum_diameter1, maximum_diameter2, (maximum_diameter1+1)/2 + (maximum_diameter2+1)/2 + 1].into_iter().max().unwrap()
    }

    fn get_adjust_list(edges: &Vec<Vec<i32>>) -> Vec<Vec<usize>> {
        let n: usize = edges.len() + 1;
        let mut result: Vec<Vec<usize>> = vec![vec![]; n];
        for edge in edges {
            result[edge[0] as usize].push(edge[1] as usize);
            result[edge[1] as usize].push(edge[0] as usize);
        }

        return result
    }

    fn find_maximum_diameter(adjust_list: &Vec<Vec<usize>>) -> i32 {
        let (index_farthest, _) = Self::bfs(0, adjust_list);
        let (_, maximum_diameter) = Self::bfs(index_farthest, adjust_list);

        return maximum_diameter
    }

    fn bfs(index_start: usize, adjust_list: &Vec<Vec<usize>>) -> (usize, i32) {
        let mut visited: HashSet<usize> = HashSet::from([index_start]);
        let mut queue: VecDeque<usize> = VecDeque::from([index_start]);
        let mut index_farthest: usize = index_start;
        let mut diameter: i32 = 0;
        while queue.len() > 0 {
            for _ in 0..queue.len() {
                let index_current: usize = queue.pop_front().unwrap();
                index_farthest = index_current;

                for &index_next in &adjust_list[index_current] {
                    if visited.contains(&index_next) {
                        continue;
                    }
                    visited.insert(index_next);

                    queue.push_back(index_next);
                }
            }

            if queue.len() > 0 {
                diameter += 1;
            }
        }

        return (index_farthest, diameter)
    }
}
```

### Solution :

Method 1 (Brute Force + DFS, ERROR: "Time Limit Exceeded", 709/723) :
```python
class Solution:
    def minimumDiameterAfterMerge(self, edges1: List[List[int]], edges2: List[List[int]]) -> int:
        n, m = len(edges1), len(edges2)
        graph1, graph2 = [[] for _ in range(n+1)], [[] for _ in range(m+1)]
        for a, b in edges1:
            graph1[a].append(b)
            graph1[b].append(a)
        for u, v in edges2:
            graph2[u].append(v)
            graph2[v].append(u)

        minimum_maximum_diameter1, maximum_maximum_diameter1 = self.get_minimum_maximum_and_maximum_maximum_diameters(graph1)
        minimum_maximum_diameter2, maximum_maximum_diameter2 = self.get_minimum_maximum_and_maximum_maximum_diameters(graph2)

        return max(maximum_maximum_diameter1, maximum_maximum_diameter2, minimum_maximum_diameter1 + minimum_maximum_diameter2 + 1)

    def get_minimum_maximum_and_maximum_maximum_diameters(self, graph: list[list[int]]) -> tuple[int, int]:
        minimum_maximum = inf
        maximum_maximum = -inf
        for index_start in range(len(graph)):
            temp = 0
            queue = deque([(index_start, index_start, 0)])
            while queue:
                index_current, index_previous, diameter = queue.popleft()

                temp = max(temp, diameter)
                for index_next in graph[index_current]:
                    if index_next == index_previous:
                        continue
                    queue.append((index_next, index_current, diameter+1))

            minimum_maximum = min(minimum_maximum, temp)
            maximum_maximum = max(maximum_maximum, temp)

        return minimum_maximum, maximum_maximum
```
