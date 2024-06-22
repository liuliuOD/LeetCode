![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1981. [Minimize The Difference Between Target And Chosen Elements](https://leetcode.com/problems/minimize-the-difference-between-target-and-chosen-elements)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M^2*N^2)$ (M: length of `matrix`, N: length of `matrix[0]`), Space Complexity: $O(M*N)$) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn minimize_the_difference(mat: Vec<Vec<i32>>, target: i32) -> i32 {
        let mut candidates: HashSet<i32> = HashSet::from_iter([0]);
        for row in mat {
            let mut temp: HashSet<i32> = HashSet::new();
            for item in row {
                for candidate in candidates.iter() {
                    temp.insert(candidate + item);
                }
            }

            candidates = temp;
        }

        return candidates.iter().map(|item| (item-target).abs()).min().unwrap()
    }
}
```

Method 2 (Hash Set + Pruning, Time Complexity: $O(M*N*P)$ (M: length of `matrix`, N: length of `matrix[0]`, P: value of `target`), Space Complexity: $O(P)$) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn minimize_the_difference(mat: Vec<Vec<i32>>, target: i32) -> i32 {
        let mut candidates: HashSet<i32> = HashSet::from([0]);
        let mut temp: HashSet<i32> = HashSet::new();
        for row in mat {
            let mut minimum_large_num: i32 = i32::MAX;
            for item in row {
                for candidate in candidates.iter() {
                    let current: i32 = candidate + item;
                    if current < target {
                        temp.insert(current);
                    } else if current < minimum_large_num {
                        minimum_large_num = current;
                    }
                }
            }

            if minimum_large_num != i32::MAX {
                temp.insert(minimum_large_num);
            }
            std::mem::swap(&mut candidates, &mut temp);
            temp.clear();
        }

        return candidates.iter().map(|item| (item-target).abs()).min().unwrap()
    }
}
```

### Solution :

Method 1 (Hash Set, Time Complexity: $O(M^2*N^2)$ (M: length of `matrix`, N: length of `matrix[0]`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def minimizeTheDifference(self, matrix: List[List[int]], target: int) -> int:
        mapping = set([0])
        for row in matrix:
            mapping_current = set()
            for item in row:
                for previous in mapping:
                    mapping_current.add(item + previous)

            mapping = mapping_current

        return min(abs(target - item) for item in mapping)
```
