![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1619. [Mean Of Array After Removing Some Elements](https://leetcode.com/problems/mean-of-array-after-removing-some-elements)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn trim_mean(arr: Vec<i32>) -> f64 {
        let n: f32 = arr.len() as f32;

        let mut arr = arr;
        arr.sort();

        let mut sum: i64 = 0;
        let mut amount: usize = 0;
        for index in ((n*0.05) as usize)..((n*0.95) as usize) {
            amount += 1;
            sum += (arr[index] as i64);
        }

        return (sum as f64) / (amount as f64)
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def trimMean(self, arr: List[int]) -> float:
        n = len(arr)
        arr.sort()
        left = int(n * 0.05)
        right = int(n * 0.95)
        total = 0
        for index in range(left, right):
            total += arr[index]

        return total / (right-left)
```

Method 2 (Binary Heap) :
```python
class Solution:
    def trimMean(self, arr: List[int]) -> float:
        n = len(arr)
        heap = arr
        heapq.heapify(arr)
        drop_left = int(n * 0.05)
        for _ in range(drop_left):
            heapq.heappop(heap)

        amount = n - drop_left*2
        total = 0
        for _ in range(amount):
            total += heapq.heappop(heap)

        return total / amount
```
