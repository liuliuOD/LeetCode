![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1791. [Find Center Of Star Graph](https://leetcode.com/problems/find-center-of-star-graph)

### Solution :

Method 1 (Greedy, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn find_center(edges: Vec<Vec<i32>>) -> i32 {
        return match edges[1].contains(&edges[0][0]) {
            true => edges[0][0],
            false => edges[0][1],
        }
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findCenter(self, edges: List[List[int]]) -> int:
        point_1, point_2, point_3 = None, None, None

        for u, v in edges:
            if u in [point_1, point_2, point_3]:
                return u
            if v in [point_1, point_2, point_3]:
                return v

            if point_1 is None:
                point_1 = u
            elif point_2 is None:
                point_2 = u
            elif point_3 is None:
                point_3 = u
            else:
                point_1 = u
            if point_1 is None:
                point_1 = v
            elif point_2 is None:
                point_2 = v
            elif point_3 is None:
                point_3 = v
            else:
                point_2 = v

        return -1
```

Method 2 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findCenter(self, edges: List[List[int]]) -> int:
        for index in range(1, len(edges)):
            if edges[index-1][0] in edges[index]:
                return edges[index-1][0]
            elif edges[index-1][1] in edges[index]:
                return edges[index-1][1]

        return -1
```

Method 3 (Greedy, Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findCenter(self, edges: List[List[int]]) -> int:
        if edges[0][0] in edges[1]:
            return edges[0][0]
        return edges[0][1]
```
