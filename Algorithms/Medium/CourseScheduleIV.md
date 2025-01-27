![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1462. [Course Schedule IV](https://leetcode.com/problems/course-schedule-iv)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded") :
```rust
impl Solution {
    pub fn check_if_prerequisite(num_courses: i32, prerequisites: Vec<Vec<i32>>, queries: Vec<Vec<i32>>) -> Vec<bool> {
        let n: usize = num_courses as usize;
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        for pair in &prerequisites {
            graph[pair[0] as usize].push(pair[1] as usize);
        }

        let mut result: Vec<bool> = Vec::new();
        for pair in queries {
            result.push(Self::is_prerequisite(pair[0] as usize, pair[1] as usize, &graph));
        }

        return result
    }

    fn is_prerequisite(start: usize, end: usize, graph: &Vec<Vec<usize>>) -> bool {
        let mut result: bool = false;
        for &index_next in &graph[start] {
            if index_next == end {
                return true
            }

            result |= Self::is_prerequisite(index_next, end, graph);
        }

        return result
    }
}
```

Method 2 (DFS + Memoization, Time Complexity: $O(M+N^2)$, Space Complexity: $O(N^2)$ (M: the number of the elements in `queries`, N: the number of the elements in `num_courses`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn check_if_prerequisite(num_courses: i32, prerequisites: Vec<Vec<i32>>, queries: Vec<Vec<i32>>) -> Vec<bool> {
        let n: usize = num_courses as usize;
        let mut graph: Vec<Vec<usize>> = vec![vec![]; n];
        for pair in &prerequisites {
            graph[pair[0] as usize].push(pair[1] as usize);
        }

        let mut memoization: HashMap<(usize, usize), bool> = HashMap::new();
        let mut result: Vec<bool> = Vec::new();
        for pair in queries {
            result.push(Self::is_prerequisite(pair[0] as usize, pair[1] as usize, &mut memoization, &graph));
        }

        return result
    }

    fn is_prerequisite(start: usize, end: usize, memoization: &mut HashMap<(usize, usize), bool>, graph: &Vec<Vec<usize>>) -> bool {
        if start == end {
            return true
        }

        let key: (usize, usize) = (start, end);
        if memoization.contains_key(&key) {
            return *memoization.get(&key).unwrap()
        }

        let mut result: bool = false;
        for &index_next in &graph[start] {
            memoization.entry((start, index_next)).or_insert(true);
            result |= Self::is_prerequisite(index_next, end, memoization, graph);
        }

        memoization.entry(key).or_insert(result);
        return result
    }
}
```

Method 3 (Floyd Warshall, Time Complexity: $O(M+N^3)$, Space Complexity: $O(N^2)$ (M: the number of the elements in `queries`, N: the number of the elements in `num_courses`)) :
```rust
impl Solution {
    pub fn check_if_prerequisite(num_courses: i32, prerequisites: Vec<Vec<i32>>, queries: Vec<Vec<i32>>) -> Vec<bool> {
        let n: usize = num_courses as usize;
        let mut dp: Vec<Vec<bool>> = vec![vec![false; n]; n];
        for pair in prerequisites {
            dp[pair[0] as usize][pair[1] as usize] = true;
        }

        for pivot in 0..n {
            for start in 0..n {
                for end in 0..n {
                    dp[start][end] |= dp[start][pivot] && dp[pivot][end];
                }
            }
        }

        return queries.into_iter()
            .map(|pair| dp[pair[0] as usize][pair[1] as usize])
            .collect::<Vec<bool>>()
    }
}
```
