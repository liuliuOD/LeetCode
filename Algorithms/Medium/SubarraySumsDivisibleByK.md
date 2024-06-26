![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 974. [Subarray Sums Divisible By K](https://leetcode.com/problems/subarray-sums-divisible-by-k)

### Solution :

Method 1 (Prefix Sum + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn subarrays_div_by_k(nums: Vec<i32>, k: i32) -> i32 {
        let mut result: i32 = 0;
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        let mut prefix_sum: i32 = 0;
        mapping.entry(0).or_insert(1);
        for num in nums {
            /* Option 1 */
            prefix_sum = (prefix_sum + num);
            if prefix_sum < 0 {
                while prefix_sum < 0 {
                    prefix_sum += k;
                }
            }
            prefix_sum %= k;
            /* Option 2

            prefix_sum = ((prefix_sum + num) % k + k) % k;
            */

            result += *mapping.entry(prefix_sum).or_default();
            mapping.entry(prefix_sum).and_modify(|value| *value += 1);
        }

        return result
    }
}
```

### Solution :

Method 1 (Prefix Sum, ERROR: "Time Limit Exceeded", 66/73) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix_sum = [0] * n
        prefix_sum[0] = nums[0]
        for index in range(1, n):
            prefix_sum[index] = prefix_sum[index-1] + nums[index]

        result = 0
        for index_left in range(n):
            for index_right in range(index_left, n):
                redundant = prefix_sum[index_left-1] if index_left > 0 else 0
                if (prefix_sum[index_right] - redundant) % k == 0:
                    result += 1

        return result
```

Method 2 (Prefix Sum + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix_sum = [0] * n
        prefix_sum[0] = nums[0]
        for index in range(1, n):
            prefix_sum[index] = nums[index] + prefix_sum[index-1]

        mapping = defaultdict(int)
        result = 0
        for index in range(n):
            """
            if x % k = n and y % k = n, then (x-y) % k = 0.
            because x = a*k + n and y = b*k + n,
            x - y = k*(a - b) + (n - n) = k*(a - b)
            """
            remainder = prefix_sum[index] % k
            # Option 1
            result += mapping[remainder] + (remainder == 0)
            """
            # Option 2

            result += remainder == 0
            result += mapping[remainder]
            """

            mapping[remainder] += 1
        return result
```

Method 3 (Prefix Sum + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix_sum = 0
        mapping = defaultdict(int)
        result = 0
        for index in range(n):
            prefix_sum += nums[index]
            remainder = prefix_sum % k
            result += mapping[remainder] + (remainder == 0)
            mapping[remainder] += 1

        return result
```

Method 4 (Prefix Sum + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        result = 0
        mapping = defaultdict(int)
        mapping[0] = 1
        prefix_sum = 0
        for num in nums:
            prefix_sum = (prefix_sum + num) % k
            # Option 1
            if prefix_sum in mapping.keys():
                result += mapping[prefix_sum]
            """
            # Option 2

            result += mapping[prefix_sum]
            """

            mapping[prefix_sum] += 1

        return result
```
