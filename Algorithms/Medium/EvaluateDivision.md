![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 399. [Evaluate Division](https://leetcode.com/problems/evaluate-division)

### Solution :

Method 1 (DFS) :
```rust
use std::collections::{ HashMap, HashSet };
impl Solution {
    pub fn calc_equation(equations: Vec<Vec<String>>, values: Vec<f64>, queries: Vec<Vec<String>>) -> Vec<f64> {
        let mut graph: HashMap<String, HashMap<String, f64>> = HashMap::new();
        for (index, equation) in equations.iter().enumerate() {
            graph.entry(equation[0].clone()).or_default().insert(equation[1].clone(), values[index]);
            graph.entry(equation[1].clone()).or_default().insert(equation[0].clone(), 1.0 / values[index]);
        }
        
        let mut results = vec![];
        let mut visited: HashSet<String> = HashSet::new();
        for query in queries.iter() {
            let result = Self::dfs(query[0].clone(), &query[1], 1.0, &graph, &mut visited);
            match result {
                Some(result) => results.push(result),
                None => results.push(-1.0),
            };
            
            visited.clear();
        }

        return results
    }

    fn dfs(start: String, goal: &String, value: f64, graph: &HashMap<String, HashMap<String, f64>>, visited: &mut HashSet<String>) -> Option<f64> {
        if !graph.contains_key(&start) {
            return None
        }
        if start.eq(goal) {
            return Some(value)
        }
        visited.insert(start.clone());

        for (neighbor, neighbor_value) in graph[&start].iter() {
            if visited.contains(neighbor) {
                continue
            }

            let result = Self::dfs(neighbor.clone(), goal, value * neighbor_value, graph, visited);
            // if we set result as -1.0, then use result != -1.0 it'll occur unexpectedly comparison result
            match result {
                Some(result) => {
                    return Some(result)
                },
                None => {
                    visited.remove(neighbor);
                },
            }
        }

        return None
    }
}
```

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        self.graph = defaultdict(dict)
        for (a, b), value in zip(equations, values):
            self.graph[a][b] = value
            self.graph[b][a] = 1 / value

        self.visited = set()
        results = []
        for start, goal in queries:
            results.append(self.dfs(start, goal, 1) if goal in self.graph else -1)
            self.visited.clear()
        return results

    def dfs(self, start: str, goal: str, value: float) -> float:
        if start == goal:
            return value

        for neighbor, neighbor_value in self.graph[start].items():
            if neighbor not in self.visited:
                self.visited.add(neighbor)

                result = self.dfs(neighbor, goal, value * neighbor_value)
                if result is not -1:
                    return result

                self.visited.remove(neighbor)
                
        # if answer not exist, return -1
        return -1
```

Method 2 (BFS) :
```python
```
