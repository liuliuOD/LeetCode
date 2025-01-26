![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2127. [Maximum Employees To Be Invited To A Meeting](https://leetcode.com/problems/maximum-employees-to-be-invited-to-a-meeting)

### Solution :

Method 1 (Graph, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `favorite`)) :
```rust
use std::collections::VecDeque;

impl Solution {
    pub fn maximum_invitations(favorite: Vec<i32>) -> i32 {
        let n: usize = favorite.len();
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        for index in 0..n {
            graph[favorite[index] as usize].push(index);
        }

        let mut longest: i32 = 0;
        let mut merged_2_cycle: i32 = 0;
        let mut visited: Vec<bool> = vec![false; n];
        for index in 0..n {
            if visited[index] {
                continue;
            }

            let mut visited_distances: Vec<i32> = vec![-1; n];
            let mut index_current: usize = index;
            let mut distance: i32 = 0;
            loop {
                if visited[index_current] {
                    break;
                }
                visited[index_current] = true;
                visited_distances[index_current] = distance;
                distance += 1;
                let index_favorite_coworker: usize = favorite[index_current] as usize;
                if visited_distances[index_favorite_coworker] == -1 {
                    index_current = index_favorite_coworker;
                    continue;
                }

                let mut distance_cycle: i32 = distance - visited_distances[index_favorite_coworker];
                longest = i32::max(longest, distance_cycle);
                if distance_cycle != 2 {
                    index_current = index_favorite_coworker;
                    continue;
                }

                let mut visited_node_in_bfs: Vec<bool> = vec![false; n];
                visited_node_in_bfs[index_current] = true;
                visited_node_in_bfs[index_favorite_coworker] = true;

                merged_2_cycle += 2;
                merged_2_cycle += Self::bfs(index_current, &mut visited_node_in_bfs, &graph);
                merged_2_cycle += Self::bfs(index_favorite_coworker, &mut visited_node_in_bfs, &graph);
                break;
            }
        }

        return i32::max(longest, merged_2_cycle)
    }

    fn bfs(index_start: usize, visited: &mut Vec<bool>, graph: &Vec<Vec<usize>>) -> i32 {
        let mut queue: VecDeque<(usize, i32)> = VecDeque::from([(index_start, 0)]);
        let mut result: i32 = 0;
        while queue.len() > 0 {
            let (index_current, distance_current) = queue.pop_front().unwrap();
            for &index_coworker in graph[index_current].iter() {
                if visited[index_coworker] {
                    continue;
                }
                visited[index_coworker] = true;

                queue.push_back((index_coworker, distance_current + 1));
                result = i32::max(result, distance_current + 1);
            }
        }

        return result
    }
}
```

Method 2 (Graph, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `favorite`)) :
```rust
use std::collections::{HashSet, HashMap, VecDeque};

impl Solution {
    pub fn maximum_invitations(favorite: Vec<i32>) -> i32 {
        let n: usize = favorite.len();
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        for index in 0..n {
            graph[favorite[index] as usize].push(index);
        }

        let mut longest: i32 = 0;
        let mut merged_2_cycle: i32 = 0;
        let mut visited: HashSet<usize> = HashSet::new();
        for index in 0..n {
            if visited.contains(&index) {
                continue;
            }

            let mut visited_distances: HashMap<usize, i32> = HashMap::new();
            let mut index_current: usize = index;
            let mut distance: i32 = 0;
            loop {
                if visited.contains(&index_current) {
                    break;
                }
                visited.insert(index_current);
                visited_distances.entry(index_current).or_insert(distance);
                distance += 1;
                let index_favorite_coworker: usize = favorite[index_current] as usize;
                if !visited_distances.contains_key(&index_favorite_coworker) {
                    index_current = index_favorite_coworker;
                    continue;
                }

                let mut distance_cycle: i32 = distance - *visited_distances.get(&index_favorite_coworker).unwrap();
                longest = i32::max(longest, distance_cycle);
                if distance_cycle != 2 {
                    index_current = index_favorite_coworker;
                    continue;
                }

                let mut visited_node_in_bfs: HashSet<usize> = HashSet::from([index_current, index_favorite_coworker]);

                merged_2_cycle += 2;
                merged_2_cycle += Self::bfs(index_current, &mut visited_node_in_bfs, &graph);
                merged_2_cycle += Self::bfs(index_favorite_coworker, &mut visited_node_in_bfs, &graph);
                break;
            }
        }

        return i32::max(longest, merged_2_cycle)
    }

    fn bfs(index_start: usize, visited: &mut HashSet<usize>, graph: &Vec<Vec<usize>>) -> i32 {
        let mut queue: VecDeque<(usize, i32)> = VecDeque::from([(index_start, 0)]);
        let mut result: i32 = 0;
        while queue.len() > 0 {
            let (index_current, distance_current) = queue.pop_front().unwrap();
            for &index_coworker in graph[index_current].iter() {
                if visited.contains(&index_coworker) {
                    continue;
                }
                visited.insert(index_coworker);

                queue.push_back((index_coworker, distance_current + 1));
                result = i32::max(result, distance_current + 1);
            }
        }

        return result
    }
}
```
