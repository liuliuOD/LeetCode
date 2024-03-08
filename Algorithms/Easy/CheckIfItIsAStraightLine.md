![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1232. [Check If It Is A Straight Line](https://leetcode.com/problems/check-if-it-is-a-straight-line)

### Solution :

Method 1 (Gradient) :
```rust
impl Solution {
    pub fn check_straight_line(coordinates: Vec<Vec<i32>>) -> bool {
        let start_x = coordinates[0][0];
        let start_y = coordinates[0][1];
        let second_x = coordinates[1][0];
        let second_y = coordinates[1][1];

        let mut result = true;
        for index in 1..coordinates.len() {
            let target_x = coordinates[index][0];
            let target_y = coordinates[index][1];
            if (start_y - target_y) * (start_x - second_x) != (start_y - second_y) * (start_x - target_x) {
                result = false;
                break;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Gradient) :
```python
class Solution:
    def checkStraightLine(self, coordinates: List[List[int]]) -> bool:
        result = True

        point_start_x, point_start_y = coordinates[0]
        point_second_x, point_second_y = coordinates[1]
        for index in range(1, len(coordinates)):
            point_temp_x, point_temp_y = coordinates[index]

            """
            Gradient between point 1 and 2: (point_start_y - point_second_y) / (point_start_x - point_second_x)
            Gradient between point 1 and N: (point_start_y - point_temp_y) / (point_start_x - point_temp_x)
            To prevent float compare problem, I use commutative law, so division change to multiplication 
            """
            if (point_start_y - point_temp_y) * (point_start_x - point_second_x) != (point_start_y - point_second_y) * (point_start_x - point_temp_x):
                result = False
                break
        return result
```
