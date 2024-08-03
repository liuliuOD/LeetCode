![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1460. [Make Two Arrays Equal By Reversing Subarrays](https://leetcode.com/problems/make-two-arrays-equal-by-reversing-subarrays)

### Solution :

Method 1 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: number of the elements in `target`)) :
```rust
impl Solution {
    pub fn can_be_equal(mut target: Vec<i32>, mut arr: Vec<i32>) -> bool {
        target.sort();
        arr.sort();
        for (a, b) in target.iter().zip(arr.iter()) {
            if a != b {
                return false
            }
        }

        return true
    }
}
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `target`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn can_be_equal(target: Vec<i32>, arr: Vec<i32>) -> bool {
        let mut map_target: HashMap<i32, i32> = HashMap::new();
        target.iter().for_each(|&value| {
            map_target.entry(value).and_modify(|item| *item += 1).or_insert(1);
        });
        let mut map_arr: HashMap<i32, i32> = HashMap::new();
        arr.iter().for_each(|&value| {
            map_arr.entry(value).and_modify(|item| *item += 1).or_insert(1);
        });

        /* Option 1 */
        for key in map_target.keys() {
            if !map_arr.contains_key(key) || map_arr[key] != map_target[key] {
                return false
            }
        }

        return true
        /* Option 2

        return map_target.iter().fold(true, |result, (key, &value)| result && map_arr.contains_key(key) && map_arr[key] == value)
        */
    }
}
```

Method 3 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: number of the elements in `target`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn can_be_equal(mut target: Vec<i32>, mut arr: Vec<i32>) -> bool {
        target.sort_unstable();
        arr.sort_unstable();

        return target == arr
    }
}
```
