![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 1700. [Number Of Students Unable To Eat Lunch](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(M+N)$ (M: length of `students`, N: length of `sandwiches`), Space Complexity: $O(1)$) :
```python
class Solution:
    def countStudents(self, students: List[int], sandwiches: List[int]) -> int:
        counter = Counter(students)
        for index, sandwich in enumerate(sandwiches):
            if sandwich in counter:
                counter[sandwich] -= 1
                if counter[sandwich] == 0:
                    del counter[sandwich]
            else:
                return len(sandwiches) - index

        return 0
```

### Solution :

Method 1 (Array, Time Complexity: $O(M+N)$ (M: length of `students`, N: length of `sandwiches`), Space Complexity: $O(1)$) :
```go
func countStudents(students []int, sandwiches []int) int {
    var counter [2]int
    for _, student := range students {
        counter[student]++
    }

    for index, sandwich := range sandwiches {
        // Option 1
        if counter[sandwich] > 0 {
            counter[sandwich]--
        } else {
            return len(sandwiches) - index
        }
        /*
        // Option 2

        if counter[sandwich] == 0 {
            return len(sandwiches) - index
        }

        counter[sandwich]--
        */
    }

    return 0
}
```
