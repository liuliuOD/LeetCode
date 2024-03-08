![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 77. [Combinations](https://leetcode.com/problems/combinations)

### Solution :

Method 1 (Backtracking) :
```rust
impl Solution {
    pub fn combine(n: i32, k: i32) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = vec![];
        Self::backtracking(vec![], 1, n, k, &mut result);
        return result
    }

    fn backtracking(combination: Vec<i32>, left: i32, right: i32, remain: i32, result: &mut Vec<Vec<i32>>) {
        if remain == 0 {
            result.push(combination);
            return
        }

        for num in left..=right {
            let mut combination_next: Vec<i32> = combination.clone();
            combination_next.push(num);
            Self::backtracking(combination_next, num+1, right, remain-1, result);
        }
    }
}
```

Method 2 (Backtracking) :
```rust
impl Solution {
    pub fn combine(n: i32, k: i32) -> Vec<Vec<i32>> {
        let mut result: Vec<Vec<i32>> = vec![];
        Self::backtracking(&mut vec![], 1, n, k, &mut result);
        return result
    }

    fn backtracking(combination: &mut Vec<i32>, left: i32, right: i32, remain: i32, result: &mut Vec<Vec<i32>>) {
        if remain == 0 {
            result.push(combination.clone());
            return
        }

        for num in left..=right {
            combination.push(num);
            Self::backtracking(combination, num+1, right, remain-1, result);
            combination.pop();
        }
    }
}
```

### Solution :

Method 1 (Backtracking) :
```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        memoization: List[List[int]] = []
        self.backtracking(memoization, 1, n, k, [])
        return memoization

    def backtracking(self, memoization: List[List[int]], start: int, end: int, remain_times: int, combination: List[int]):
        if remain_times == 0:
            memoization.append(combination)
            return None

        if start > end:
            return None

        for num in range(start, end+1):
            self.backtracking(memoization, num+1, end, remain_times-1, combination+[num])
```

Method 2 (Backtracking) :
```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        self.combination = []
        self.result: List[List[int]] = []
        self.backtracking(1, n, k)

        return self.result

    def backtracking(self, start: int, end: int, remain: int):
        if remain == 0:
            self.result.append(self.combination.copy())
            return None

        for num in range(start, end+1):
            self.combination.append(num)
            self.backtracking(num+1, end, remain-1)
            self.combination.pop()
```
