![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 791. [Custom Sort String](https://leetcode.com/problems/custom-sort-string)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def customSortString(self, order: str, s: str) -> str:
        counter = Counter(s)
        result = ''
        for key in order:
            if key not in counter.keys():
                continue

            result += key * counter[key]
            del counter[key]

        for key, amount in counter.items():
            result += key * amount

        return result
```

Method 2 (List, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
BASE: int = ord('a')

class Solution:
    def customSortString(self, order: str, s: str) -> str:
        counter = [0] * 26
        for char in s:
            counter[ord(char)-BASE] += 1

        result = ''
        for key in order:
            index = ord(key) - BASE
            if counter[index] == 0:
                continue

            result += key * counter[index]
            counter[index] = 0

        for offset, amount in enumerate(counter):
            result += chr(BASE+offset) * amount

        return result
```

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func customSortString(order string, s string) string {
    counter := make(map[rune]int)
    for _, char := range s {
        counter[char]++
    }

    result := make([]rune, len(s))
    index := 0
    for _, char := range order {
        amount, ok := counter[char]
        if ok {
            for i := 0; i < amount; i++ {
                result[index] = char
                index++
            }
            delete(counter, char)
        }
    }

    for char, amount := range counter {
        for i := 0; i < amount; i++ {
            result[index] = char
            index++
        }
    }

    return string(result)
}
```

Method 2 (Array, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func customSortString(order string, s string) string {
    counter := [26]int{}
    for _, char := range s {
        counter[char-'a']++
    }

    result := make([]rune, len(s))
    index := 0
    for _, char := range order {
        index_char := char - 'a'
        for i := 0; i < counter[index_char]; i++ {
            result[index] = char
            index++
        }
        counter[index_char] = 0
    }

    for offset, amount := range counter {
        for i := 0; i < amount; i++ {
            result[index] = 'a' + rune(offset)
            index++
        }
    }

    return string(result)
}
```
