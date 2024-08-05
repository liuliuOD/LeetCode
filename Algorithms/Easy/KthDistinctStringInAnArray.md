![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2053. [Kth Distinct String In An Array](https://leetcode.com/problems/kth-distinct-string-in-an-array)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `arr`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn kth_distinct(arr: Vec<String>, k: i32) -> String {
        let mut map: HashMap<String, u16> = HashMap::new();
        arr.iter().for_each(|item| {
            map.entry(item.clone()).and_modify(|number| *number += 1).or_insert(1);
        });

        let mut amount_distinct: u16 = 0;
        for item in arr.iter() {
            if map[item] > 1 {
                continue;
            }

            amount_distinct += 1;
            if amount_distinct == k as u16 {
                return item.to_string()
            }
        }
        return "".to_string()
    }
}
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `arr`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn kth_distinct(arr: Vec<String>, k: i32) -> String {
        let mut map: HashMap<&String, usize> = HashMap::new();
        arr.iter().for_each(|item| {
            map.entry(item).and_modify(|number| *number += 1).or_insert(1);
        });

        let mut amount_distinct: usize = 0;
        for item in arr.iter() {
            /* Option 1 */
            if *map.get(item).unwrap() > 1 {
            /* Option 2

            if map[item] > 1 {
            */
                continue;
            }

            amount_distinct += 1;
            if amount_distinct == k as usize {
                return item.to_string()
            }
        }
        return "".to_string()
    }
}
```
