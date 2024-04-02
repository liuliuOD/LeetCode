![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 205. [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    # Option 1
    def isIsomorphic(self, s: str, t: str) -> bool:
        mapping_s = dict()
        order_s = 0
        temp_s = ''
        for char in s:
            if char not in mapping_s:
                mapping_s[char] = str(order_s)
                order_s += 1

            temp_s += mapping_s[char] + '-'

        mapping_t = dict()
        order_t = 0
        temp_t = ''
        for char in t:
            if char not in mapping_t:
                mapping_t[char] = str(order_t)
                order_t += 1

            temp_t += mapping_t[char] + '-'

        return temp_s == temp_t
    """
    # Option 2

    def isIsomorphic(self, s: str, t: str) -> bool:
        return self.getOrder(s) == self.getOrder(t)

    def getOrder(self, string: str) -> str:
        result = ''

        mapping = dict()
        order = 0
        for char in string:
            if char not in mapping:
                mapping[char] = str(order)
                order += 1

            result += mapping[char] + '-'

        return result
    """
```

Method 2 (Array, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        mapping_s = [-1] * 128
        mapping_t = [-1] * 128
        n = len(s)
        if n != len(t):
            return False

        for index in range(n):
            ascii_s = ord(s[index])
            ascii_t = ord(t[index])
            if mapping_s[ascii_s] != mapping_t[ascii_t]:
                return False

            mapping_s[ascii_s] = index
            mapping_t[ascii_t] = index

        return True
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func isIsomorphic(s string, t string) bool {
    return getOrder(s) == getOrder(t)
}

func getOrder(target string) string {
    result := ""
    mapping := make(map[rune]string)
    symbol := 0
    for _, char := range target {
        value, ok := mapping[char]
        if !ok {
            mapping[char] = string(symbol)
            symbol++
        }

        result += value + "-"
    }

    return result
}
```

Method 2 (Array, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func isIsomorphic(s string, t string) bool {
    var mappingS [128]int
    var mappingT [128]int
    n := len(s)
    if n != len(t) {
        return false
    }

    for index := 0; index < n; index++ {
        asciiS := int(s[index])
        asciiT := int(t[index])
        if mappingS[asciiS] != mappingT[asciiT] {
            return false
        }

        mappingS[asciiS] = index + 1
        mappingT[asciiT] = index + 1
    }

    return true
}
```
