![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 373. [Find K Pairs With Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums)

### Solution :

Method 1 (Minimum Heap) :
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;
impl Solution {
    pub fn k_smallest_pairs(nums1: Vec<i32>, nums2: Vec<i32>, mut k: i32) -> Vec<Vec<i32>> {
        let mut minimum_heap: BinaryHeap<(Reverse<i32>, usize)> = BinaryHeap::new();
        for n1 in nums1 {
            if minimum_heap.len() == k as usize {
                break;
            }
            minimum_heap.push((Reverse(n1+nums2[0]), 0));
        }
        
        let mut result: Vec<Vec<i32>> = vec![];
        while k > 0 && minimum_heap.len() > 0 {
            let (Reverse(sum_pair), index_n2) = minimum_heap.pop().unwrap();
            let n2 = nums2[index_n2];
            let n1 = sum_pair - n2;
            result.push(vec![n1, n2]);

            let index_next_n2: usize = index_n2 + 1;
            if index_next_n2 < nums2.len() {
                minimum_heap.push((Reverse(n1 + nums2[index_next_n2]), index_next_n2));
            }

            k -= 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Brute Force, ERROR: "Memory Limit Exceeded") :
```python
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        pairs = []
        for index_1 in range(len(nums1)):
            for index_2 in range(len(nums2)):
                pairs.append([nums1[index_1], nums2[index_2]])
        pairs.sort(key=lambda x: x[0]+x[1], reverse=True)

        result = []
        while pairs and k:
            result.append(pairs.pop())
            k -= 1
        return result
```

Method 2 ([Minimum Heap](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/solutions/3686980/from-dumb-to-pro-with-just-one-visit-my-promise-to-you-with-efficient-selection-of-k-smallest-pair/)) :
```python
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        heap = []
        for n1 in nums1:
            if len(heap) == k:
                break
            heapq.heappush(heap, [n1+nums2[0], 0])
        
        result = []
        while k and heap:
            k -= 1
            sum_pair, index_n2 = heapq.heappop(heap)
            n1 = sum_pair - nums2[index_n2]
            result.append([n1, nums2[index_n2]])

            index_next_n2 = index_n2 + 1
            if index_next_n2 < len(nums2):
                heapq.heappush(heap, [n1+nums2[index_next_n2], index_next_n2])
        return result
```
