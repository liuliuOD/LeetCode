![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1496. [Path Crossing](https://leetcode.com/problems/path-crossing)

### Solution :

Method 1 :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn is_path_crossing(path: String) -> bool {
        let mut x: i32 = 0;
        let mut y: i32 = 0;
        let mut visited: HashSet<(i32, i32)> = HashSet::new();
        visited.insert((x, y));
        for directive in path.chars() {
            match directive {
                'N' => x -= 1,
                'S' => x += 1,
                'E' => y += 1,
                'W' => y -= 1,
                _ => (),
            };

            if visited.contains(&(x, y)) {
                return true
            }
            visited.insert((x, y));
        }

        return false
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isPathCrossing(self, path: str) -> bool:
        current = (0, 0)
        visited = set([current])
        for move in path:
            if move == 'N':
                current = (current[0]-1, current[1])
            if move == 'S':
                current = (current[0]+1, current[1])
            if move == 'E':
                current = (current[0], current[1]+1)
            if move == 'W':
                current = (current[0], current[1]-1)

            if current in visited:
                return True
            visited.add(current)

        return False
```

Method 2 (Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isPathCrossing(self, path: str) -> bool:
        n = len(path)
        for index_start in range(n):
            x = y = 0
            for index_next in range(index_start, n):
                move = path[index_next]
                if move == 'N':
                    x += 1
                if move == 'S':
                    x -= 1
                if move == 'E':
                    y += 1
                if move == 'W':
                    y -= 1

                if x == 0 == y:
                    return True

        return False
```
