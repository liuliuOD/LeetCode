![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 486. [Predict The Winner](https://leetcode.com/problems/predict-the-winner)

### Solution :

Method 1 (DFS + Memoization) :
```rust
use std::cmp::{min, max};
impl Solution {
    pub fn predict_the_winner(nums: Vec<i32>) -> bool {
        let n: usize = nums.len();
        let mut memoization: Vec<Vec<i32>> = vec![vec![-999; n]; n];

        return Self::get_score_difference(0, n-1, true, &mut memoization, &nums) >= 0
    }

    fn get_score_difference(index_left: usize, index_right: usize, is_turn_player1: bool, memoization: &mut Vec<Vec<i32>>, nums: &Vec<i32>) -> i32 {
        let n: usize = nums.len();
        if index_left >= n || index_right >= n || index_left > index_right {
            return 0
        }

        if memoization[index_left][index_right] != -999 {
            return memoization[index_left][index_right]
        }

        let mut choose_left: i32 = nums[index_left];
        let mut choose_right: i32 = nums[index_right];
        if !is_turn_player1 {
            choose_left *= -1;
            choose_right *= -1;
        }

        let next_turn: bool = !is_turn_player1;
        choose_left += Self::get_score_difference(index_left+1, index_right, next_turn, memoization, nums);
        choose_right += Self::get_score_difference(index_left, index_right-1, next_turn, memoization, nums);

        memoization[index_left][index_right] = if is_turn_player1 {
            max(choose_left, choose_right)
        } else {
            min(choose_left, choose_right)
        };

        return memoization[index_left][index_right]
    }
}
```

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def PredictTheWinner(self, nums: List[int]) -> bool:
        n = len(nums)
        self.memoization = [[None]*n for _ in range(n)]

        return self.scoreDifference(0, n-1, True, nums) >= 0

    def scoreDifference(self, pointer_left: int, pointer_right: int, is_turn_player1: bool, nums: List[int]) -> int:
        if pointer_left > pointer_right:
            return 0

        if self.memoization[pointer_left][pointer_right] is not None:
            return self.memoization[pointer_left][pointer_right]

        next_turn = not is_turn_player1

        choose_left = nums[pointer_left]
        choose_right = nums[pointer_right]
        if not is_turn_player1:
            choose_left *= -1
            choose_right *= -1

        choose_left += self.scoreDifference(pointer_left+1, pointer_right, next_turn, nums)
        choose_right += self.scoreDifference(pointer_left, pointer_right-1, next_turn, nums)

        result = max(choose_left, choose_right) if is_turn_player1 else min(choose_left, choose_right)

        self.memoization[pointer_left][pointer_right] = result
        return self.memoization[pointer_left][pointer_right]
```
