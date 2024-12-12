![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2558. [Take Gifts From The Richest Pile](https://leetcode.com/problems/take-gifts-from-the-richest-pile)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(M*Log(N)+N*Log(N))$, Space Complexity: $O(N)$ (M: the value of `k`, N: the number of the elements in `gifts`)) :
```Rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn pick_gifts(gifts: Vec<i32>, k: i32) -> i64 {
        let mut heap: BinaryHeap<i64> = BinaryHeap::from_iter(gifts.into_iter().map(|num| num as i64));
        for _ in 0..k {
            if let Some(num) = heap.pop() {
                heap.push((num as f64).sqrt() as i64);
            }
        }

        return heap.into_iter().sum()
    }
}
```

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(M*Log(N)+N*Log(N))$, Space Complexity: $O(N)$ (M: the value of `k`, N: the number of the elements in `gifts`)) :
```java
class Solution {
    public long pickGifts(int[] gifts, int k) {
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        for (int num: gifts) {
            queue.add(-num);
        }

        while (k-- > 0) {
            int num = -queue.poll();
            queue.add((int) -Math.sqrt(num));
        }

        long result = 0;
        while (!queue.isEmpty()) {
            result -= queue.poll();
        }

        return result;
    }
}
```
