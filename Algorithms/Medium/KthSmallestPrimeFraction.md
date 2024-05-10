![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 786. [K-th Smallest Prime Fraction](https://leetcode.com/problems/k-th-smallest-prime-fraction)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N^2)$, Space Complexity: $O(K)$) :
```rust
use std::cmp::Ord;
use std::cmp::Ordering;
use std::cmp::PartialOrd;
use std::collections::BinaryHeap;

#[derive(Debug)]
struct Fraction(i32, i32);
impl Fraction {
    fn get(&self) -> f32 {
        return self.0 as f32 / self.1 as f32
    }

    fn result(&self) -> Vec<i32> {
        return vec![self.0, self.1]
    }
}
impl Ord for Fraction {
    fn cmp(&self, another: &Self) -> Ordering {
        return self.get().partial_cmp(&another.get()).unwrap_or(Ordering::Equal)
    }
}
impl PartialOrd for Fraction {
    fn partial_cmp(&self, another: &Self) -> Option<Ordering> {
        return Some(self.cmp(another))
    }
}
impl Eq for Fraction {}
impl PartialEq<Self> for Fraction {
    fn eq(&self, another: &Self) -> bool {
        return self.get() == another.get()
    }
}

impl Solution {
    pub fn kth_smallest_prime_fraction(arr: Vec<i32>, k: i32) -> Vec<i32> {
        let mut heap: BinaryHeap<Fraction> = BinaryHeap::new();
        let n: usize = arr.len();
        for index_left in 0..n {
            for index_right in index_left+1..n {
                heap.push(Fraction(arr[index_left], arr[index_right]));

                if heap.len() > k as usize {
                    heap.pop();
                }
            }
        }

        return heap.pop().unwrap().result()
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$) :
```python
class Solution:
    def kthSmallestPrimeFraction(self, arr: List[int], k: int) -> List[int]:
        n = len(arr)
        fractions = [(arr[i] / arr[j], arr[i], arr[j]) for i in range(n) for j in range(i+1, n)]
        fractions.sort(key=lambda item: item[0])
        return list(fractions[k-1][1:])
```

Method 2 (Binary Heap, Time Complexity: $O(N^2)$, Space Complexity: $O(K)$) :
```python
class Solution:
    def kthSmallestPrimeFraction(self, arr: List[int], k: int) -> List[int]:
        n = len(arr)
        heap = []
        for i in range(n):
            for j in range(i+1, n):
                heapq.heappush(heap, (-arr[i] / arr[j], arr[i], arr[j]))
                while len(heap) > k:
                    heapq.heappop(heap)

        return list(heapq.heappop(heap)[1:])
```
