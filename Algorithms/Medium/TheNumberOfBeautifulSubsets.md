![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2597. [The Number Of Beautiful Subsets](https://leetcode.com/problems/the-number-of-beautiful-subsets)

### Solution :

Method 1 (backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn beautiful_subsets(nums: Vec<i32>, k: i32) -> i32 {
        let mut memoization: HashMap<i32, i32> = HashMap::new();
        let mut result: i32 = 0;
        Self::backtracking(0, &mut result, &mut memoization, &nums, k);
        return result - 1
    }

    fn backtracking(index: usize, result: &mut i32, memoization: &mut HashMap<i32, i32>, nums: &Vec<i32>, k: i32) {
        let n: usize = nums.len();
        if index >= n {
            *result += 1;
            return
        }

        let num: i32 = nums[index];
        Self::backtracking(index+1, result, memoization, nums, k);
        if *memoization.entry(num).or_default() == 0 {
            *memoization.entry(num-k).or_default() += 1;
            *memoization.entry(num+k).or_default() += 1;

            Self::backtracking(index+1, result, memoization, nums, k);

            *memoization.entry(num-k).or_default() -= 1;
            *memoization.entry(num+k).or_default() -= 1;
        }
    }
}
```

### Solution :

Method 1 (Bitmask + Brute Force, ERROR: "Time Limit Exceeded", 56 / 1307, Time Complexity: $O(N^2*2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        n = len(nums)
        result = 0
        for bitwise in range(1, 1 << n):
            subset = []
            for index in range(n):
                if ((1 << index) & bitwise) == 0:
                    continue

                for num in subset:
                    if abs(num - nums[index]) == k:
                        break
                else:
                    subset.append(nums[index])
                    continue

                break
            else:
                result += 1
        return result
```

Method 2 (Bitmask + Hash Set, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        n = len(nums)
        result = 0
        for bitwise in range(1, 1 << n):
            may_non_beautiful: set[int] = set()
            for index in range(n):
                if ((1 << index) & bitwise) == 0:
                    continue

                current = nums[index]
                if current in may_non_beautiful:
                    break

                may_non_beautiful.add(current - k)
                may_non_beautiful.add(current + k)
            else:
                result += 1
        return result
```

Method 3 (backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def beautifulSubsets(self, nums: List[int], k: int) -> int:
        self.result = 0
        memoization = defaultdict(int)
        self.backtracking(0, memoization, nums, k)
        return self.result - 1

    def backtracking(self, index: int, memoization: dict[int, int], nums: list[int], k: int):
        n = len(nums)
        if index >= n:
            self.result += 1
            return

        num = nums[index]
        if num not in memoization:
            add_k = num + k
            minus_k = num - k
            memoization[minus_k] += 1
            memoization[add_k] += 1
            self.backtracking(index+1, memoization, nums, k)
            memoization[minus_k] -= 1
            memoization[add_k] -= 1
            if memoization[minus_k] == 0:
                del memoization[minus_k]
            if memoization[add_k] == 0:
                del memoization[add_k]

        self.backtracking(index+1, memoization, nums, k)
```
