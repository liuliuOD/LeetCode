![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 857. [Minimum Cost To Hire K Workers](https://leetcode.com/problems/minimum-cost-to-hire-k-workers)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N+K)$) :
```rust
use std::cmp::Ord;
use std::cmp::Ordering;
use std::cmp::PartialOrd;
use std::collections::BinaryHeap;

#[derive(Debug)]
struct Fraction(i32, i32, usize);
impl Fraction {
    fn get(&self) -> f64 {
        return self.0 as f64 / self.1 as f64
    }
}
impl Eq for Fraction {}
impl PartialEq<Self> for Fraction {
    fn eq(&self, another: &Self) -> bool {
        return self.get() == another.get()
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

impl Solution {
    pub fn mincost_to_hire_workers(quality: Vec<i32>, wage: Vec<i32>, k: i32) -> f64 {
        let k: usize = k as usize;
        let n: usize = quality.len();
        let mut fractions: Vec<Fraction> = vec![];
        for index in 0..n {
            fractions.push(Fraction(wage[index], quality[index], index));
        }
        fractions.sort();

        let mut result: f64 = f64::MAX;
        let mut heap: BinaryHeap<i32> = BinaryHeap::new();
        let mut sum_quality: i32 = 0;
        for index in 0..n {
            let current: &Fraction = &fractions[index];
            heap.push(current.1);
            sum_quality += current.1;
            if heap.len() > k {
                sum_quality -= heap.pop().unwrap();
            }
            if heap.len() == k {
                result = result.min(fractions[index].get() * sum_quality as f64);
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 41/46, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def mincostToHireWorkers(self, quality: List[int], wage: List[int], k: int) -> float:
        n = len(quality)
        fraction = [(wage[index] / quality[index], index) for index in range(n)]

        result = inf
        fraction.sort()
        for index in range(k-1, n):
            current = fraction[index]
            cost = current[0]
            candidates = [cost * quality[current[1]]]
            for index_previous in range(index):
                previous = fraction[index_previous]
                candidates.append(cost * quality[previous[1]])
            candidates.sort()
            result = min(result, sum(candidates[:k]))

        return result
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N+K)$) :
```python
class Solution:
    def mincostToHireWorkers(self, quality: List[int], wage: List[int], k: int) -> float:
        n = len(quality)
        fraction = [(wage[index] / quality[index], index) for index in range(n)]
        fraction.sort()

        result = inf
        heap = []
        choose_quality_sum = 0
        for index in range(n):
            current = fraction[index]
            cost = current[0]
            current_quality = quality[current[1]]
            choose_quality_sum += current_quality
            heapq.heappush(heap, -current_quality)
            if len(heap) > k:
                choose_quality_sum += heapq.heappop(heap)
            if len(heap) == k:
                result = min(result, cost * choose_quality_sum)

        return result
```
