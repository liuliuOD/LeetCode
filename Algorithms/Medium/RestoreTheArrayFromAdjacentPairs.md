![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1743. [Restore The Array From Adjacent Pairs](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs)

### Solution :

Method 1 (Recursive DFS) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn restore_array(adjacent_pairs: Vec<Vec<i32>>) -> Vec<i32> {
        let mut graph: HashMap<i32, Vec<i32>> = HashMap::new();
        for index in 0..adjacent_pairs.len() {
            let a = adjacent_pairs[index][0];
            let b = adjacent_pairs[index][1];
            graph.entry(a).or_insert(vec![]).push(b);
            graph.entry(b).or_insert(vec![]).push(a);
        }

        let mut result: Vec<i32> = vec![];
        for key in graph.keys() {
            if graph[key].len() != 1 {
                continue;
            }

            Self::dfs(*key, None, &mut result, graph);
            break;
        }

        return result
    }

    fn dfs(current: i32, previous: Option<i32>, result: &mut Vec<i32>, graph: HashMap<i32, Vec<i32>>) {
        result.push(current);
        for &next in graph[&current].iter() {
            /* Option 1 */
            if let Some(previous) = previous {
                if previous == next {
                    continue;
                }
            }
            /* Option 2

            match previous {
                Some(previous) => if previous == next {
                    continue;
                },
                _ => (),
            };
            */
            Self::dfs(next, Some(current), result, graph);
            break;
        }
    }
}
```

Method 2 (Iterative DFS) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn restore_array(adjacent_pairs: Vec<Vec<i32>>) -> Vec<i32> {
        let mut graph: HashMap<i32, Vec<i32>> = HashMap::new();
        for index in 0..adjacent_pairs.len() {
            let a = adjacent_pairs[index][0];
            let b = adjacent_pairs[index][1];
            graph.entry(a).or_insert(vec![]).push(b);
            graph.entry(b).or_insert(vec![]).push(a);
        }

        for key in graph.keys() {
            if graph[key].len() != 1 {
                continue;
            }

            let mut current: i32 = *key;
            let mut previous: Option<i32> = None;
            let mut result: Vec<i32> = vec![current];
            while result.len() < graph.len() {
                for &next in graph[&current].iter() {
                    match previous {
                        Some(previous) => if previous == next {
                            continue;
                        },
                        _ => (),
                    };

                    result.push(next);
                    previous = Some(current);
                    current = next;
                    break;
                }
            }

            return result
        }

        unreachable!()
    }
}
```

### Solution :

Method 1 (Recursive DFS + Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def restoreArray(self, adjacent_pairs: List[List[int]]) -> List[int]:
        n = len(adjacent_pairs) + 1
        graph = defaultdict(list)
        ingress = defaultdict(int)
        for a, b in adjacent_pairs:
            ingress[a] += 1
            ingress[b] += 1

            graph[a].append(b)
            graph[b].append(a)

        self.result = []
        starts = [key for key, amount in ingress.items() if amount == 1]
        # Option 1
        for start in starts:
            self.dfs(start, set(), graph)
            break
        """
        # Option 2

        self.dfs(starts[0], set(), graph)
        """

        return self.result

    def dfs(self, current: int, visited: Set[int], graph: List[List[int]]):
        if current in visited:
            return
        visited.add(current)

        self.result.append(current)
        for index_next in graph[current]:
            self.dfs(index_next, visited, graph)
```

Method 2 (Recursive DFS + Set) :
```python
class Solution:
    def restoreArray(self, adjacent_pairs: List[List[int]]) -> List[int]:
        n = len(adjacent_pairs) + 1
        graph = defaultdict(list)
        for a, b in adjacent_pairs:
            graph[a].append(b)
            graph[b].append(a)

        result = []
        for key in graph.keys():
            if len(graph[key]) == 1:
                self.dfs(key, set(), result, graph)
                return result

        return []

    def dfs(self, current: int, visited: Set[int], result: List[int], graph: List[List[int]]):
        if current in visited:
            return
        visited.add(current)

        result.append(current)
        for index_next in graph[current]:
            self.dfs(index_next, visited, result, graph)
```

Method 3 (Recursive DFS) :
```python
class Solution:
    def restoreArray(self, adjacent_pairs: List[List[int]]) -> List[int]:
        n = len(adjacent_pairs) + 1
        graph = defaultdict(list)
        for a, b in adjacent_pairs:
            graph[a].append(b)
            graph[b].append(a)

        result = []
        for key in graph.keys():
            if len(graph[key]) == 1:
                self.dfs(key, None, result, graph)
                return result

        return []

    def dfs(self, current: int, previous: Optional[int], result: List[int], graph: List[List[int]]):
        result.append(current)
        for index_next in graph[current]:
            if previous == index_next:
                continue

            self.dfs(index_next, current, result, graph)
```

Method 4 (Iterative DFS) :
```python
class Solution:
    def restoreArray(self, adjacent_pairs: List[List[int]]) -> List[int]:
        graph = defaultdict(list)
        for a, b in adjacent_pairs:
            graph[a].append(b)
            graph[b].append(a)

        current = list(filter(lambda key: len(graph[key]) == 1, graph.keys()))[0]
        previous = None
        result = [current]
        while len(result) < len(graph):
            for child in graph[current]:
                if child == previous:
                    continue

                result.append(child)
                previous = current
                current = child
                break

        return result
```
