![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2070. [Most Beautiful Item For Each Query](https://leetcode.com/problems/most-beautiful-item-for-each-query)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(M*Log(M)+N*Log(N))$, Space Complexity: $O(M+N)$ (M: the number of the elements in `queries`, N: the number of the elements in `items`)) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn maximum_beauty(mut items: Vec<Vec<i32>>, queries: Vec<i32>) -> Vec<i32> {
        let m: usize = queries.len();
        let n: usize = items.len();
        items.sort();
        let mut queries_sorted: Vec<usize> = (0..m).collect();
        queries_sorted.sort_by_key(|index| queries[*index]);
        let mut heap: BinaryHeap<i32> = BinaryHeap::new();
        let mut index_items: usize = 0;
        let mut result: Vec<i32> = vec![0; m];
        for index in queries_sorted.into_iter() {
            while index_items < n && items[index_items][0] <= queries[index] {
                heap.push(items[index_items][1]);
                index_items += 1;
            }

            if heap.len() > 0 {
                result[index] = *heap.peek().unwrap();
            }
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(M*Log(M)+N*Log(N))$, Space Complexity: $O(M+N)$ (M: the number of the elements in `queries`, N: the number of the elements in `items`)) :
```rust
impl Solution {
    pub fn maximum_beauty(mut items: Vec<Vec<i32>>, queries: Vec<i32>) -> Vec<i32> {
        let m: usize = queries.len();
        let n: usize = items.len();
        items.sort();
        let mut queries_sorted: Vec<usize> = (0..m).collect();
        queries_sorted.sort_by_key(|index| queries[*index]);
        let mut most_beautiful: i32 = 0;
        let mut index_items: usize = 0;
        let mut result: Vec<i32> = vec![0; m];
        for index in queries_sorted.into_iter() {
            while index_items < n && items[index_items][0] <= queries[index] {
                most_beautiful = i32::max(most_beautiful, items[index_items][1]);
                index_items += 1;
            }

            result[index] = most_beautiful;
        }

        return result
    }
}
```
