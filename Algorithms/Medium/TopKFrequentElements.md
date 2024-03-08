![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 347. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)

### Solution :

Method 1 :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn top_k_frequent(nums: Vec<i32>, k: i32) -> Vec<i32> {
        let mut map: HashMap<i32, i16> = HashMap::new();
        for &num in nums.iter() {
            *map.entry(num).or_default() += 1;
        }

        let mut sorted = map.into_iter().collect::<Vec<_>>();
        sorted.sort_by(|left, right| right.1.cmp(&left.1));

        sorted.into_iter().map(|item| item.0).collect::<Vec<i32>>()[..k as usize].to_vec()
    }
}
```

### Solution :

Method 1 :
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = defaultdict(lambda: 0)
        # also can use counter = defaultdict(int)
        for num in nums:
            counter[num] += 1

        return map(lambda item: item[0], sorted(counter.items(), key=lambda item: item[1], reverse=True)[:k])
```
