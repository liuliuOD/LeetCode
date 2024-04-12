![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 42. [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn trap(height: Vec<i32>) -> i32 {
        let mut result: i32 = 0;
        let mut stack: Vec<usize> = Vec::new();
        for (index_right, &h_right) in height.iter().enumerate() {
            while stack.len() > 0 && height[*stack.last().unwrap()] < h_right {
                let h_previous: i32 = height[stack.pop().unwrap()];
                if stack.len() == 0 {
                    break
                }

                let index_left: usize = *stack.last().unwrap();
                let h_left: i32 = height[index_left];
                result += (h_left.min(h_right) - h_previous) * (index_right - index_left - 1) as i32;
            }

            stack.push(index_right);
        }

        return result
    }
}
```

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = []
        result = 0
        for index_right, h_right in enumerate(height):
            while stack and height[stack[-1]] < h_right:
                h_middle = height[stack.pop()]
                if stack:
                    index_left = stack[-1]
                    h_left = height[index_left]
                    result += (min(h_left, h_right) - h_middle) * (index_right - index_left - 1)

            stack.append(index_right)

        return result
```

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func trap(height []int) int {
    var result int
    var stack []int
    for index_right, h := range height {
        for n := len(stack); n > 0 && height[stack[n-1]] < h; n = len(stack) {
            h_previous := height[stack[n-1]]
            stack = stack[:n-1]
            if n <= 1 {
                break
            }

            index_left := stack[n-2]
            result += (min(height[index_left], h) - h_previous) * (index_right - index_left - 1)
        }

        stack = append(stack, index_right)
    }

    return result
}
```
