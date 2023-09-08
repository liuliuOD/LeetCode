![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 118. [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle)

### Solution :

Method 1 (Dynamic Programming) :
```rust
impl Solution {
    pub fn generate(num_rows: i32) -> Vec<Vec<i32>> {
        let num_rows: usize = num_rows as usize;
        let mut result: Vec<Vec<i32>> = vec![vec![]; num_rows];

        for row in 0..num_rows {
            for column in 0..row+1 {
                if column == 0 || column == row {
                    result[row].push(1);
                    continue;
                }
                let temp: i32 = result[row-1][column-1] + result[row-1][column];
                result[row].push(temp);
            }
        }
        return result
    }
}
```

### Solution :

Method 1 (Dynamic Programming) :
```python
class Solution:
    def generate(self, num_rows: int) -> List[List[int]]:
        dp = [[1] for _ in range(num_rows)]
        for index in range(1, num_rows):
            for index_num in range(1, index+1):
                value = 0
                if index_num < len(dp[index-1]):
                    value += dp[index-1][index_num]
                if index_num-1 >= 0:
                    value += dp[index-1][index_num-1]

                dp[index].append(value)
        return dp
```

### Solution :

Method 1 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param Integer $numRows
     * @return Integer[][]
     */
    function generate($numRows) {
        $dp = [[1]];
        for ($index=1; $index < $numRows; $index++) {
            $row = [1];
            $previousRow = $dp[$index-1];
            for ($indexColumn = 1; $indexColumn < $index+1; $indexColumn++) {
                $row[] = $previousRow[$indexColumn-1] + $previousRow[$indexColumn];
            }
            $dp[] = $row;
        }

        return $dp;
    }
}
```
