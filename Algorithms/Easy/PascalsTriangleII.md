![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 119. [Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii)

### Solution :

Method 1 (Dynamic Programming) :
```rust
impl Solution {
    pub fn get_row(row_index: i32) -> Vec<i32> {
        let row_index: usize = row_index as usize;
        let mut dp: Vec<i32> = vec![1];
        let mut result: Vec<i32> = vec![];
        for index_row in 0..row_index+1 {
            result = vec![];
            for index_column in 0..index_row+1 {
                if index_column == 0 || index_column == index_row {
                    result.push(1);
                    continue;
                }

                result.push(dp[index_column-1] + dp[index_column]);
            }
            dp = result.clone();
        }

        return result
    }
}
```

### Solution :

Method 1 (Dynamic Programming, Space Complexity: $O(N)$) :
```python
class Solution:
    def getRow(self, row_index: int) -> List[int]:
        dp = [1]
        for amount in range(1, row_index+2):
            temp = []
            for index in range(amount):
                item = 0
                if index == 0:
                    item += dp[0]
                elif index >= len(dp):
                    item += dp[-1]
                else:
                    item += dp[index-1] + dp[index]

                temp.append(item)

            dp = temp

        return dp
```
