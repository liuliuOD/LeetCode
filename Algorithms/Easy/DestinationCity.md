![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1436. [Destination City](https://leetcode.com/problems/destination-city)

### Solution :

Method 1 :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn dest_city(paths: Vec<Vec<String>>) -> String {
        let mut mapping_out: HashSet<&String> = HashSet::new();

        for path in paths.iter() {
            mapping_out.insert(&path[0]);
        }

        for path in paths.iter() {
            if mapping_out.contains(&path[1]) {
                continue;
            }

            return path[1].clone()
        }

        unreachable!()
    }
}
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def destCity(self, paths: List[List[str]]) -> str:
        mapping_out: Dict[str, int] = defaultdict(int)
        for start, end in paths:
            mapping_out[start] += 1
            # let end be recorded in `mapping_out`
            mapping_out[end]

        for result, amount in mapping_out.items():
            if amount == 0:
                return result
```

Method 2 (Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$):
```python
class Solution:
    def destCity(self, paths: List[List[str]]) -> str:
        mapping_out: Set[str] = set()
        for start, _ in paths:
            mapping_out.add(start)

        for _, end in paths:
            if end not in mapping_out:
                return end
```
