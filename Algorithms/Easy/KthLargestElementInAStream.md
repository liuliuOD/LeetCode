![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 703. [Kth Largest Element In A Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream)

### Solution :

```rust
/**
 * Your KthLargest object will be instantiated and called as such:
 * let obj = KthLargest::new(k, nums);
 * let ret_1: i32 = obj.add(val);
 */
```

Method 1 :
```rust
struct KthLargest {
    k: usize,
    nums: Vec<i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl KthLargest {

    fn new(k: i32, nums: Vec<i32>) -> Self {
        Self {
            k: k as usize,
            nums: nums,
        }
    }
    
    fn add(&mut self, val: i32) -> i32 {
        self.nums.push(val);
        Self::sort(self);
        return self.nums[self.k - 1]
    }

    fn sort(&mut self) {
        self.nums.sort_by(|left, right| right.cmp(left));
    }
}
```

Method 2 (Minimum Heap) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

struct KthLargest {
    k: usize,
    min_heap: BinaryHeap<Reverse<i32>>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl KthLargest {

    fn new(k: i32, nums: Vec<i32>) -> Self {
        let k = k as usize;
        let mut heap = BinaryHeap::new();
        for &n in nums.iter() {
            heap.push(Reverse(n));
        }
        while heap.len() > k {
            heap.pop();
        }

        return Self {
            k: k,
            min_heap: heap,
        }
    }
    
    fn add(&mut self, val: i32) -> i32 {
        self.min_heap.push(Reverse(val));
        if self.min_heap.len() > self.k {
            self.min_heap.pop();
        }

        return match self.min_heap.peek() {
            Some(Reverse(result)) => *result,
            None => 0,
        }
    }
}
```

### Solution :

```python
# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)
```

Method 1 :
```python
class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        self.k = k
        self.nums = nums
        self.nums.sort()

    def add(self, val: int) -> int:
        self.nums.append(val)
        self.nums.sort()
        return self.nums[-self.k]
```

Method 2 (Minimum Heap) :
```python
class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        self.k = k
        self.min_heap = []
        heapq.heapify(nums)
        while len(nums) > k:
            heapq.heappop(nums)
        self.min_heap = nums

    def add(self, val: int) -> int:
        heapq.heappush(self.min_heap, val)
        if len(self.min_heap) > self.k:
            heapq.heappop(self.min_heap)

        return self.min_heap[0]
```
