![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1557. [Minimum Number Of Vertices To Reach All Nodes](https://leetcode.com/problems/minimum-number-of-vertices-to-reach-all-nodes)

### Solution :

Method 1 (HashSet) :
```rust
use std::collections::HashSet;
use std::iter::FromIterator;
impl Solution {
    pub fn find_smallest_set_of_vertices(n: i32, edges: Vec<Vec<i32>>) -> Vec<i32> {
        let mut vertices: HashSet<i32> = HashSet::from_iter((0..n).collect::<Vec<i32>>());
        for edge in edges.iter() {
            vertices.remove(&edge[1]);
        }

        return vertices.into_iter().collect::<Vec<i32>>()
    }
}
```

### Solution :

Method 1 (List + Loop) :
```python
class Solution:
    def findSmallestSetOfVertices(self, n: int, edges: List[List[int]]) -> List[int]:
        vertices = [True] * n
        for edge in edges:
            vertices[edge[1]] = False
        
        result = []
        for (index, v) in enumerate(vertices):
            if v:
                result.append(index)
        return result
```

Method 2 (set + difference) :
```python
class Solution:
    def findSmallestSetOfVertices(self, n: int, edges: List[List[int]]) -> List[int]:
        vertices = set(range(n))
        vertices_incoming = set(incoming for _, incoming in edges)

        return list(vertices - vertices_incoming)
```

Method 3 (set + lambda) :
```python
class Solution:
    def findSmallestSetOfVertices(self, n: int, edges: List[List[int]]) -> List[int]:
        vertices_incoming = set(incoming for _, incoming in edges)

        return list(filter(lambda vertex: vertex not in vertices_incoming, range(n)))
```
