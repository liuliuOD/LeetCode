![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1249. [Minimum Remove To Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        result = ""
        depth = 0
        for char in s:
            if char == '(':
                depth += 1
            elif char == ')':
                depth -= 1

            if depth < 0:
                depth = 0
                continue

            result += char

        if depth == 0:
            return result

        temp = result
        result = ""
        for char in reversed(temp):
            if depth > 0 and char == '(':
                depth -= 1
                continue

            result += char

        return result[::-1]
```

Method 2 (Array, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        left = []
        right = []
        for index, char in enumerate(s):
            if char == '(':
                left.append(index)
            if char == ')':
                if left:
                    left.pop()
                else:
                    right.append(index)

        result = ""
        for index in range(len(s)):
            if index in left or index in right:
                continue

            result += s[index]

        return result
```

Method 3 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        left = []
        right = []
        for index, char in enumerate(s):
            if char == '(':
                left.append(index)
            if char == ')':
                if left:
                    left.pop()
                else:
                    right.append(index)

        result = ""
        index_removal = set(left+right)
        for index in range(len(s)):
            if index in index_removal:
                continue

            result += s[index]

        return result
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func minRemoveToMakeValid(s string) string {
    var left, right []int
    for index, char := range s {
        if char == '(' {
            left = append(left, index)
        } else if char == ')' {
            if len(left) > 0 {
                left = left[:len(left)-1]
            } else {
                right = append(right, index)
            }
        }
    }

    index_removal := make(map[int]bool)
    for _, index := range left {
        index_removal[index] = true
    }
    for _, index := range right {
        index_removal[index] = true
    }

    var result []rune
    for index, char := range s {
        _, ok := index_removal[index]
        if ok {
            continue
        }

        result = append(result, char)
    }

    return string(result)
}
```

Method 2 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
type parenthese struct {
    isLeft bool
    index int
}
func minRemoveToMakeValid(s string) string {
    var stack []parenthese
    for index, char := range s {
        if char == '(' {
            stack = append(stack, parenthese{true, index})
        } else if char == ')' {
            if len(stack) > 0 && stack[len(stack)-1].isLeft {
                stack = stack[:len(stack)-1]
            } else {
                stack = append(stack, parenthese{false, index})
            }
        }
    }

    var result []byte
    index_stack := 0
    for index := 0; index < len(s); index++ {
        if index_stack < len(stack) && stack[index_stack].index == index {
            index_stack++
            continue
        }

        result = append(result, s[index])
    }

    return string(result)
}
```
