![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2870. [Minimum Number Of Operations To Make Array Empty](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-empty)

### Solution :

Method 1 :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn min_operations(nums: Vec<i32>) -> i32 {
        let mut counter: HashMap<i32, i32> = HashMap::new();
        for num in nums {
            /* Option 1 */
            counter.entry(num).and_modify(|value| *value += 1).or_insert(1);
            /* Option 2
            
            *counter.entry(num).or_insert(0) += 1;
            */
        }

        let mut result: i32 = 0;
        for (_, amount) in counter {
            if amount <= 1 {
                return -1
            }

            match amount % 3 {
                0 => result += amount / 3,
                1 | 2 => result += 1 + amount / 3,
                _ => (),
            };
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int]) -> int:
        nums.sort()
        nums.append(1_000_001)
        result = 0
        left = 0
        for right in range(len(nums)):
            if nums[right] == nums[left]:
                continue

            amount = right - left
            if amount < 2:
                return -1

            # Option 1
            if amount % 3 == 0:
                result += amount // 3
            elif amount % 3 == 1:
                result += 2 + (amount - 3) // 3
            elif amount % 3 == 2:
                result += 1 + amount // 3
            """
            # Option 2

            if amount % 3 == 0:
                result += amount // 3
            elif amount % 3 in [1, 2]:
                result += 1 + amount // 3
            """
            """
            # Option 3

            result += amount // 3 + (1 if amount % 3 != 0 else 0)
            """

            left = right

        return result
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int]) -> int:
        counter = Counter(nums)
        result = 0
        for amount in counter.values():
            if amount < 2:
                return -1

            result += amount // 3 + (1 if amount % 3 != 0 else 0)

        return result
```
