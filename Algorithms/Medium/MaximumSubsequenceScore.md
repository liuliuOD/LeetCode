![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2542. [Maximum Subsequence Score](https://leetcode.com/problems/maximum-subsequence-score)

### Solution :

Method 1 (Minimum Heap) :
```rust
use std::collections::BinaryHeap;
use std::cmp::{ Reverse, max };

impl Solution {
    pub fn max_score(nums1: Vec<i32>, nums2: Vec<i32>, k: i32) -> i64 {
        let mut nums: Vec<(i32, i32)> = vec![];
        for (&n1, &n2) in nums1.iter().zip(nums2.iter()) {
            nums.push((n1, n2));
        }
        nums.sort_by_key(|item| -item.1);

        let mut heap: BinaryHeap<Reverse<i32>> = BinaryHeap::new();
        let mut temp = 0;
        let mut result = 0;
        for &(n1, n2) in nums.iter() {
            temp += n1 as i64;
            heap.push(Reverse(n1));

            if heap.len() < k as usize {
                continue;
            }

            if heap.len() > k as usize {
                if let Some(Reverse(item)) = heap.pop() {
                    temp -= item as i64;
                }
            }
            result = max(result, temp * n2 as i64);
        }

        return result
    }
}
```

### Solution :

Method 1 (DFS, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def maxScore(self, nums1: List[int], nums2: List[int], k: int) -> int:
        self.nums1 = nums1
        self.nums2 = nums2
        result = 0
        for id_n1 in range(len(nums1)):
            result = max(result, self.dfs([id_n1], k - 1))
        return result

    def dfs(self, ids, step) -> int:
        result = 0
        if step == 0:
            min_num2 = 10**5
            for id in ids:
                result += self.nums1[id]
                min_num2 = min(min_num2, self.nums2[id])
            return result * min_num2

        for i in range(ids[-1] + 1, len(self.nums1)):
            result = max(result, self.dfs(ids + [i], step - 1))
        return result
```

Method 2 (Heap) :
```python
class Solution:
    def maxScore(self, nums1: List[int], nums2: List[int], k: int) -> int:
        group = zip(nums1, nums2)
        group = sorted(group, key=lambda item: -item[-1])

        min_heap = []
        temp = 0
        result = 0
        for pair in group:
            n1, n2 = pair
            heappush(min_heap, n1)
            temp += n1
            if len(min_heap) > k:
                temp -= heappop(min_heap)
            if len(min_heap) == k:
                result = max(result, temp * n2)

        return result
```
