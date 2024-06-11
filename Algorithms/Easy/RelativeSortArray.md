![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1122. [Relative Sort Array](https://leetcode.com/problems/relative-sort-array)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M+N*Log(N))$ (M: length of `arr1`, N: length of `arr2`), Space Complexity: $O(M)$) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn relative_sort_array(arr1: Vec<i32>, arr2: Vec<i32>) -> Vec<i32> {
        let mut counter: HashMap<i32, i32> = HashMap::new();
        for num in arr1 {
            counter.entry(num).and_modify(|value| *value += 1).or_insert(1);
        }

        let mut result: Vec<i32> = vec![];
        for num in arr2 {
            result.extend(vec![num; *counter.get(&num).unwrap() as usize]);
            counter.remove(&num);
        }

        let mut num_remaining: Vec<i32> = counter.clone().into_keys().collect();
        num_remaining.sort();
        for num in num_remaining {
            result.extend(vec![num; *counter.get(&num).unwrap() as usize]);
        }

        return result
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M+N*Log(N))$ (M: length of `arr1`, N: length of `arr2`), Space Complexity: $O(M)$) :
```python
class Solution:
    def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
        counter = Counter(arr1)
        result = []
        for num in arr2:
            result.extend([num]*counter[num])
            del counter[num]

        for num in sorted(counter.keys()):
            result.extend([num]*counter[num])

        return result
```

Method 2 (Brute Force, Time Complexity: $O(N+M*Log(M))$ (M: length of `arr1`, N: length of `arr2`), Space Complexity: $O(N)$) :
```python
class Solution:
    def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
        mapping = {num: index for index, num in enumerate(arr2)}
        return sorted(arr1, key=lambda num: (mapping.get(num, inf), num))
```
