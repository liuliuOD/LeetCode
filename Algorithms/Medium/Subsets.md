![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 78. [Subsets](https://leetcode.com/problems/subsets)

### Solution :

Method 1 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = vec![];
        Self::backtracking(0, &mut vec![], &mut result, &nums);
        return result
    }

    fn backtracking(index: usize, subset: &mut Vec<i32>, result: &mut Vec<Vec<i32>>, nums: &Vec<i32>) {
        if index >= nums.len() {
            result.push(subset.clone());
            return
        }

        Self::backtracking(index+1, subset, result, nums);
        subset.push(nums[index]);
        Self::backtracking(index+1, subset, result, nums);
        subset.pop();
    }
}
```

Method 2 (Bitwise, Time Complexity: $O(N*2^N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = vec![];
        let n: usize = nums.len();
        for bitwise in 0..(1 << n) {
            let mut subset: Vec<i32> = vec![];
            for index in 0..n {
                if (1 << index) & bitwise > 0 {
                    subset.push(nums[index]);
                }
            }

            result.push(subset);
        }

        return result
    }
}
```

### Solution :

Method 1 (Backtracking, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        self.result = []

        self.backtracking(0, [], nums)
        return self.result

    def backtracking(self, index: int, subset: list[int], nums: list[int]):
        if index >= len(nums):
            self.result.append(subset.copy())
            return

        subset.append(nums[index])
        self.backtracking(index+1, subset, nums)
        subset.pop()
        self.backtracking(index+1, subset, nums)
```

Method 2 (Built-In method, Time Complexity: $O(N*2^N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # Option 1
        result = []
        for amount in range(len(nums)+1):
            result.extend(combinations(nums, amount))

        return result
        """
        # Option 2

        return reduce(lambda result, amount: result + list(combinations(nums, amount)), range(len(nums)+1), [])
        """
```

Method 3 (Bitwise, Time Complexity: $O(N*2^N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        result = []
        for bitwise in range(1 << n):
            subset = []
            for index in range(n):
                if (1 << index) & bitwise:
                    subset.append(nums[index])

            result.append(subset)

        return result
```
