![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 215. [Kth Largest Element In An Array](https://leetcode.com/problems/kth-largest-element-in-an-array)

### Solution :

Method 1 (Heap) :
```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;
impl Solution {
    pub fn find_kth_largest(nums: Vec<i32>, k: i32) -> i32 {
        let mut heap: BinaryHeap<Reverse<i32>> = BinaryHeap::new();
        for &num in nums.iter() {
            heap.push(Reverse(num));

            if heap.len() > k as usize {
                heap.pop();
            }
        }

        return match heap.pop().unwrap() {
            Reverse(result) => result,
            _ => 0,
        }
    }
}
```

Method 2 (Quick Select) :
```rust
impl Solution {
    pub fn find_kth_largest(mut nums: Vec<i32>, k: i32) -> i32 {
        let k: usize = k as usize;
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = n - 1;

        loop {
            let index_pivot: usize = left + (right-left) / 2;
            let index_pivot_next: usize = Self::quick_sort(index_pivot, left, right, &mut nums);

            if index_pivot_next == n-k {
                return nums[index_pivot_next]
            }
            else if index_pivot_next < n-k {
                left = index_pivot_next + 1;
            }
            else if index_pivot_next > n-k {
                right = index_pivot_next - 1;
            }
        }
    }

    fn quick_sort(index_pivot: usize, index_left: usize, index_right: usize, nums: &mut Vec<i32>) -> usize {
        let pivot: i32 = nums[index_pivot];
        nums.swap(index_pivot, index_right);
        let mut pointer: usize = index_left;

        for index in index_left..index_right {
            if nums[index] >= pivot {
                continue;
            }

            nums.swap(index, pointer);
            pointer += 1;
        }

        nums.swap(index_right, pointer);
        return pointer
    }
}
```

Method 3 (Quick Select) :
```rust
impl Solution {
    pub fn find_kth_largest(mut nums: Vec<i32>, k: i32) -> i32 {
        let k: usize = k as usize;
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = n - 1;

        loop {
            let index_pivot: usize = left + (right-left) / 2;
            let index_pivot_next: usize = Self::quick_sort(index_pivot, left, right, &mut nums);

            if index_pivot_next == n-k {
                return nums[index_pivot_next]
            }
            else if index_pivot_next < n-k {
                left = index_pivot_next + 1;
            }
            else if index_pivot_next > n-k {
                right = index_pivot_next - 1;
            }
        }
    }

    fn quick_sort(index_pivot: usize, index_left: usize, index_right: usize, nums: &mut Vec<i32>) -> usize {
        let pivot: i32 = nums[index_pivot];
        nums.swap(index_pivot, index_left);
        let mut pointer: usize = index_right;

        for index in (index_left+1..=index_right).rev() {
            if nums[index] <= pivot {
                continue;
            }

            nums.swap(index, pointer);
            pointer -= 1;
        }

        nums.swap(index_left, pointer);
        return pointer
    }
}
```

### Solution :

Method 1 (Native Sort) :
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # 1.
        nums.sort(reverse=True)
        return nums[k-1]

        """
        2.
        return sorted(nums, reverse=True)[k-1]
        """
```

Method 2 (Heap) :
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = []
        for num in nums:
            heapq.heappush(heap, num)
            if len(heap) > k:
                heapq.heappop(heap)
        return heap[0]
```

Method 3 (Quick Select) :
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        n = len(nums)
        left = 0
        right = n - 1
        while left <= right:
            pivot = left + (right-left) // 2
            index_pivot = self.quickSort(pivot, left, right, nums)

            if index_pivot == n-k:
                return nums[index_pivot]
            elif index_pivot < n-k:
                left = index_pivot + 1
            elif index_pivot > n-k:
                right = index_pivot - 1

        return nums[left]

    def quickSort(self, pivot: int, left: int, right: int, nums: List[int]) -> int:
        value_pivot = nums[pivot]
        # swap pivot to right-side
        nums[pivot], nums[right] = nums[right], nums[pivot]
        pointer = left

        for index in range(left, right):
            if nums[index] < value_pivot:
                nums[index], nums[pointer] = nums[pointer], nums[index]
                pointer += 1
        nums[right], nums[pointer] = nums[pointer], nums[right]
        return pointer
```

### Solution :

Method 1 (Min Heap) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer
     */
    function findKthLargest($nums, $k) {
        $minHeap = new SplMinHeap();
        foreach ($nums as $num) {
            $minHeap->insert($num);
            if ($minHeap->count() > $k) {
                $minHeap->extract();
            }
        }

        return $minHeap->top();
    }
}
```

Method 2 (Min Heap) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer
     */
    function findKthLargest($nums, $k) {
        $minHeap = new SplMaxHeap();
        foreach ($nums as $num) {
            $minHeap->insert(-$num);
            if ($minHeap->count() > $k) {
                $minHeap->extract();
            }
        }

        return -$minHeap->top();
    }
}
```
