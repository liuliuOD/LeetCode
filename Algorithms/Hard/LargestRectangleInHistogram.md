![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 84. [Largest Rectangle In Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram)

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn largest_rectangle_area(heights: Vec<i32>) -> i32 {
        let n: usize = heights.len();
        let mut stack: Vec<usize> = vec![];

        let mut index_left: Vec<i32> = vec![-1; n];
        for (index, &height) in heights.iter().enumerate() {
            while stack.len() > 0 && heights[*stack.last().unwrap()] >= height {
                stack.pop();
            }
            if stack.len() > 0 {
                index_left[index] = *stack.last().unwrap() as i32;
            }         

            stack.push(index);
        }

        stack = vec![];
        let mut index_right: Vec<i32> = vec![n as i32; n];
        for index in (0..n).rev() {
            while stack.len() > 0 && heights[*stack.last().unwrap()] >= heights[index] {
                stack.pop();
            }
            if stack.len() > 0 {
                index_right[index] = *stack.last().unwrap() as i32;
            }

            stack.push(index);
        }

        let mut result: i32 = 0;
        for (index, &height) in heights.iter().enumerate() {
            result = result.max(height * (index_right[index] - index_left[index] - 1));
        }

        return result
    }
}
```

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        n = len(heights)
        index_left = [-1] * n
        stack = []
        for index in range(n):
            while stack and heights[stack[-1]] >= heights[index]:
                stack.pop()
            if stack:
                index_left[index] = stack[-1]

            stack.append(index)

        index_right = [n] * n
        stack = []
        for index in reversed(range(n)):
            while stack and heights[stack[-1]] >= heights[index]:
                stack.pop()
            if stack:
                index_right[index] = stack[-1]

            stack.append(index)

        result = 0
        for index in range(n):
            result = max(result, heights[index] * (index_right[index] - index_left[index] - 1))

        return result
```

### Solution :

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func largestRectangleArea(heights []int) int {
    var n int = len(heights)
    stack := make([]int, 0, n)

    index_left := make([]int, n)
    for index, height := range heights {
        for n_stack := len(stack); n_stack > 0 && heights[stack[n_stack-1]] >= height; n_stack-- {
            stack = stack[:n_stack-1]
        }
        n_stack := len(stack)
        if n_stack > 0 {
            index_left[index] = stack[n_stack-1]
        } else {
            index_left[index] = -1
        }

        stack = append(stack, index)
    }

    stack = stack[:0]
    index_right := make([]int, n)
    for index := n-1; index >= 0; index-- {
        for n_stack := len(stack); n_stack > 0 && heights[stack[n_stack-1]] >= heights[index]; n_stack-- {
            stack = stack[:n_stack-1]
        }
        n_stack := len(stack)
        if n_stack > 0 {
            index_right[index] = stack[n_stack-1]
        } else {
            index_right[index] = n
        }

        stack = append(stack, index)
    }

    var result int
    for index, height := range heights {
        result = max(result, height * (index_right[index] - index_left[index] - 1))
    }

    return result
}
```
