![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1614. [Maximum Nesting Depth Of The Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxDepth(self, s: str) -> int:
        result = depth = 0
        for char in s:
            if char == '(':
                depth += 1
            elif char == ')':
                depth -= 1

            result = max(result, depth)

        return result
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func maxDepth(s string) int {
    result, depth := 0, 0
    for _, char := range s {
        if char == '(' {
            depth++
            result = max(result, depth)
        } else if char == ')' {
            depth--
        }
    }

    return result
}
```
