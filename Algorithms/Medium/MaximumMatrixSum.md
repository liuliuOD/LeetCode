![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1975. [Maximum Matrix Sum](https://leetcode.com/problems/maximum-matrix-sum)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```rust
impl Solution {
    pub fn max_matrix_sum(matrix: Vec<Vec<i32>>) -> i64 {
        let mut result: i64 = 0;
        let mut existed_negative: bool = false;
        let mut minimum: i64 = i64::MAX;
        for row in matrix {
            for element in row {
                let positive: i64 = element.abs() as i64;
                result += positive;
                minimum = i64::min(minimum, positive);
                if element < 0 {
                    existed_negative = !existed_negative;
                }
            }
        }

        return if existed_negative && minimum != 0 {
            result - 2*minimum
        } else {
            result
        }
    }
}
```

### Solution :

Method 1 (Greedy, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of the elements in `matrix`, N: the number of the elements in `matrix[0]`)) :
```java
class Solution {
    public long maxMatrixSum(int[][] matrix) {
        boolean remainNegative = false;
        long result = 0;
        int minimum = Integer.MAX_VALUE;
        for (int[] row: matrix) {
            for (int element: row) {
                int positive = Math.abs(element);
                result += positive;
                minimum = Math.min(minimum, positive);
                if (element < 0) {
                    remainNegative = !remainNegative;
                }
            }
        }

        if (remainNegative && minimum != 0) {
            return result - 2*minimum;
        }
        return result;
    }
}
```
