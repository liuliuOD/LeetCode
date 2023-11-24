![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1561. [Maximum Number Of Coins You Can Get](https://leetcode.com/problems/maximum-number-of-coins-you-can-get)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn max_coins(mut piles: Vec<i32>) -> i32 {
        piles.sort();
        let n: usize = piles.len();
        let mut result: i32 = 0;
        let mut visited: usize = 0;
        while visited < n {
            piles.pop();
            result += piles.pop().unwrap();
            visited += 3;
        }

        return result
    }
}
```

Method 2 (Binary Heap) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn max_coins(piles: Vec<i32>) -> i32 {
        let n: usize = piles.len();
        let mut heap: BinaryHeap<i32> = BinaryHeap::from(piles);
        let mut visited: usize = 0;
        let mut result: i32 = 0;
        while visited < n {
            heap.pop();
            result += heap.pop().unwrap();
            visited += 3;
        }

        return result
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn max_coins(mut piles: Vec<i32>) -> i32 {
        let n: usize = piles.len();

        piles.sort();
        /* Option 1 */
        return piles.iter()
            .enumerate()
            .filter(|&(index, _)| index >= n/3 && (n-index)%2 == 0)
            .map(|(index, value)| value)
            .sum()
        /* Option 2

        return piles.iter().skip(n/3).step_by(2).sum()
        */
        /* Option 3

        return piles[n/3..].iter().step_by(2).sum()
        */
    }
}
```

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxCoins(self, piles: List[int]) -> int:
        n = len(piles)
        max_heap = list(map(lambda value: -value, piles))
        heapq.heapify(max_heap)
        result = 0
        visited = 0
        while visited < n:
            heapq.heappop(max_heap)
            result -= heapq.heappop(max_heap)

            visited += 3

        return result
```

Method 2 (Dequeue, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxCoins(self, piles: List[int]) -> int:
        piles.sort()
        piles = deque(piles)
        result = 0
        while piles:
            piles.pop()
            result += piles.pop()
            piles.popleft()

        return result
```

Method 3 :
```python
class Solution:
    def maxCoins(self, piles: List[int]) -> int:
        n = len(piles)
        piles.sort()
        result = 0
        for index in range(n//3, n, 2):
            result += piles[index]

        return result
```
