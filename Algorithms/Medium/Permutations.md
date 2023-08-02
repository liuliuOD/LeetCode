![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 46. [Permutations](https://leetcode.com/problems/permutations)

### Solution :

Method 1 (Backtracking) :
```rust
impl Solution {
    pub fn permute(nums: Vec<i32>) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = vec![];
        Self::backtracking(0, &nums, &mut vec![], &mut result);

        return result
    }

    fn backtracking(bitmask: usize, nums: &Vec<i32>, permutation: &mut Vec<i32>, result: &mut Vec<Vec<i32>>) {
        if bitmask == (1 << nums.len())-1 {
            result.push(permutation.clone());
            return
        }

        for index in 0..nums.len() {
            let current_mask = 1 << index;
            if (bitmask & current_mask) != 0 {
                continue;
            }

            permutation.push(nums[index]);
            Self::backtracking(bitmask | current_mask, nums, permutation, result);
            permutation.pop();
        }
    }
}
```

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result: List[List[int]] = []
        self.dfs(nums, [], result)

        return result

    def dfs(self, candidate: List[int], permutation: List[int], result: List[List[int]]):
        if len(candidate) == 0:
            result.append(permutation)
            return None

        for index in range(len(candidate)):
            self.dfs(candidate[:index]+candidate[index+1:], permutation+[candidate[index]], result)
```

Method 2 (Backtracking) :
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result: List[List[int]] = []
        self.backtracking(nums, result, [])

        return result

    def backtracking(self, candidate: List[int], result: List[List[int]], permutation: List[int]):
        if len(candidate) == 0:
            result.append(permutation.copy())
            return None

        for index in range(len(candidate)):
            permutation.append(candidate[index])
            self.backtracking(candidate[:index]+candidate[index+1:], result, permutation)
            permutation.pop()
```

Method 3 (Backtracking + Bitmask) :
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result: List[List[int]] = []
        self.backtracking(nums, 0, result, [])

        return result

    def backtracking(self, nums: List[int], bitmask: int, result: List[List[int]], permutation: List[int]):
        if bitmask == ((1 << len(nums)) - 1):
            result.append(permutation.copy())
            return None

        for index in range(len(nums)):
            if bitmask & (1 << index):
                continue

            permutation.append(nums[index])
            self.backtracking(nums, bitmask | (1 << index), result, permutation)
            permutation.pop()
```
