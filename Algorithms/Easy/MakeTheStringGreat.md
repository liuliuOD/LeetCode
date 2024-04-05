![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1544. [Make The String Great](https://leetcode.com/problems/make-the-string-great)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def makeGood(self, s: str) -> str:
        result = s
        while self.isBad(result):
            result = self.remove(result)

        return result

    def isBad(self, s: str) -> bool:
        for index in range(len(s)-1):
            if self.badAdjacency(s[index], s[index+1]):
                return True

        return False

    def remove(self, s: str) -> str:
        for index in range(len(s)-1):
            if self.badAdjacency(s[index], s[index+1]):
                return s[:index] + s[index+2:]

        return ""

    def badAdjacency(self, a: str, b: str) -> bool:
        return a.lower() == b.lower() and ((a.islower() and b.isupper()) or (a.isupper() and b.islower()))
```

### Solution :

Method 1 (Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```go
func makeGood(s string) string {
    length := len(s)
    for true {
        for index := 0; index < len(s)-1; index++ {
            if abs(int(s[index])-int(s[index+1])) == 32 {
                s = s[:index] + s[index+2:]
                break
            }
        }

        if length == len(s) {
            break
        }
        length = len(s)
    }

    return s
}

func abs(num int) int {
    if num < 0 {
        return -num
    }

    return num
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func makeGood(s string) string {
    var stack []rune
    for _, char := range s {
        if len(stack) > 0 && abs(int(stack[len(stack)-1])-int(char)) == 32 {
            stack = stack[:len(stack)-1]
        } else {
            stack = append(stack, char)
        }
    }

    return string(stack)
}

func abs(num int) int {
    if num < 0 {
        return -num
    }
    return num
}
```
