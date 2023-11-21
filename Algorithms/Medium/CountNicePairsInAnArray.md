![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1814. [Count Nice Pairs In An Array](https://leetcode.com/problems/count-nice-pairs-in-an-array)

### Hint :

```text
nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])
can be transferred to
nums[i] - rev(nums[i]) == nums[j] - rev(nums[j])
```

### Solution :

Method 1 :
```rust
use std::collections::HashMap;

const MODULO: i32 = 1_000_000_007;
impl Solution {
    pub fn count_nice_pairs(nums: Vec<i32>) -> i32 {
        let mut result: i32 = 0;
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        for num in nums {
            /* Option 1 */
            let num_reversed: i32 = num.to_string().chars().rev().collect::<String>().parse().unwrap();
            /* Option 2
            
            let num_reversed: i32 = num.to_string().chars().rev().collect::<String>().parse::<i32>().unwrap();
            */
            let key_mapping: i32 = num - num_reversed;
            result = (result + *mapping.entry(key_mapping).or_default()) % MODULO;
            mapping.entry(key_mapping).and_modify(|value| *value += 1).or_insert(1);
        }

        return result
    }
}
```

Method 2 :
```rust
use std::collections::HashMap;

const MODULO: i32 = 1_000_000_007;
impl Solution {
    pub fn count_nice_pairs(nums: Vec<i32>) -> i32 {
        let mut result: i32 = 0;
        let mut mapping: HashMap<i32, i32> = HashMap::new();
        for num in nums {
            let num_reversed: i32 = Self::reverse_i32(num);
            let key_mapping: i32 = num - num_reversed;
            /* Option 1 */
            result = (result + *mapping.entry(key_mapping).or_default()) % MODULO;
            mapping.entry(key_mapping).and_modify(|value| *value += 1).or_insert(1);
            /* Option 2

            let item: &mut i32 = mapping.entry(key_mapping).or_default();
            result = (result + *item) % MODULO;
            *item += 1;
            */
        }

        return result
    }

    fn reverse_i32(mut num: i32) -> i32 {
        let mut result: i32 = 0;
        while num > 0 {
            result = result*10 + num%10;
            num /= 10;
        }

        return result
    }
}
```

### Solution :

Method 1 (Hash Map + Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        nums_reversed = []
        for num in nums:
            num_reversed = 0
            while num:
                num_reversed *= 10
                num_reversed += num % 10
                num //= 10

            nums_reversed.append(num_reversed)

        n = len(nums)
        pairs_sum = defaultdict(list)
        for index in range(n):
            pairs_sum[nums[index]-nums_reversed[index]].append(index)

        MODULO = 1_000_000_007
        result = 0
        for index in range(n):
            index_pairs_sum = nums[index] - nums_reversed[index]
            position = bisect.bisect_left(pairs_sum[index_pairs_sum], index)
            result += len(pairs_sum[index_pairs_sum]) - position - 1
            result %= MODULO

        return result
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        nums_reversed = []
        for num in nums:
            num_reversed = 0
            while num:
                num_reversed *= 10
                num_reversed += num % 10
                num //= 10

            nums_reversed.append(num_reversed)

        MODULO = 1_000_000_007
        n = len(nums)
        result = 0
        pairs_sum = defaultdict(int)
        for index in range(n):
            result += pairs_sum[nums[index]-nums_reversed[index]]
            result %= MODULO
            pairs_sum[nums[index]-nums_reversed[index]] += 1

        return result
```

Method 3 :
```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        MODULO = 1_000_000_007
        n = len(nums)
        result = 0
        pairs_sum = defaultdict(int)
        for index in range(n):
            num_reversed = 0
            # Option 1
            num = nums[index]
            while num:
                num_reversed *= 10
                num_reversed += num % 10
                num //= 10

            result += pairs_sum[nums[index]-num_reversed]
            result %= MODULO
            pairs_sum[nums[index]-num_reversed] += 1
            """
            # Option 2

            num = temp = nums[index]
            while temp:
                num_reversed *= 10
                num_reversed += temp % 10
                temp //= 10

            result += pairs_sum[num-num_reversed]
            result %= MODULO
            pairs_sum[num-num_reversed] += 1
            """

        return result
```

Metho 4 :
```python
class Solution:
    def countNicePairs(self, nums: List[int]) -> int:
        MODULO = 1_000_000_007
        n = len(nums)
        result = 0
        pairs_sum = defaultdict(int)
        # Option 1
        for index in range(n):
            num = nums[index]
        """
        # Option 2

        for num in nums:
        """
            # The integer can be reversed without too much memory usage by converting it to a string
            num_reversed = int(str(num)[::-1])

            result += pairs_sum[num-num_reversed]
            result %= MODULO
            pairs_sum[num-num_reversed] += 1

        return result
```
