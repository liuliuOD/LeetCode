![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 3047. [Find The Largest Area Of Square Inside Two Rectangles](https://leetcode.com/problems/find-the-largest-area-of-square-inside-two-rectangles)

### Solution :

Method 1 (In weekly contest 386, Brute Force) :
```python
class Solution:
    def largestSquareArea(self, bottomLeft: List[List[int]], topRight: List[List[int]]) -> int:
        n = len(bottomLeft)
        result = 0
        for index in range(n):
            x_start, y_start = bottomLeft[index]
            x_end, y_end = topRight[index]
            for index_next in range(n):
                if index == index_next:
                    continue

                x_next_start, y_next_start = bottomLeft[index_next]
                x_next_end, y_next_end = topRight[index_next]
                if x_next_start <= x_start <= x_next_end and y_next_start <= y_start <= y_next_end and x_next_start <= x_end <= x_next_end and y_next_start <= y_end <= y_next_end:
                    result = max(result, min(x_end-x_start, y_end-y_start)**2)
                elif x_start <= x_next_start <= x_end and y_start <= y_next_start <= y_end and x_next_end <= x_end and y_next_end <= y_end:
                    result = max(result, min(x_next_end-x_next_start, y_next_end-y_next_start)**2)
                elif y_next_start <= y_start <= y_next_end and (x_next_start <= x_start <= x_next_end or x_next_start <= x_end <= x_next_end or (x_start < x_next_start and x_end > x_next_end)):
                    result = max(result, min(y_next_end-y_start, y_end-y_start, y_next_end-y_next_start, min(x_end, x_next_end)-max(x_start, x_next_start))**2)
                elif x_start <= x_next_start <= x_end and (y_start <= y_next_start <= y_end or y_start <= y_next_end <= y_end or (y_next_start < y_start and y_next_end > y_end)):
                    result = max(result, min(x_end-x_next_start, x_end-x_start, x_next_end-x_next_start, min(y_end, y_next_end)-max(y_start, y_next_start))**2)
                elif y_next_start <= y_end <= y_next_end and (x_start <= x_next_start <= x_end or x_start <= x_next_end <= x_end or (x_next_start < x_start and x_next_end > x_end)):
                    result = max(result, min(y_end-y_next_start, y_end-y_start, y_next_end-y_next_start, min(x_end, x_next_end)-max(x_start, x_next_start))**2)
                elif x_start <= x_next_end <= x_end and (y_start <= y_next_start <= y_end or y_start <= y_next_end <= y_end or (y_next_start < y_start and y_next_end > y_end)):
                    result = max(result, min(x_next_end-x_start, x_end-x_start, x_next_end-x_next_start, min(y_end, y_next_end)-max(y_start, y_next_start))**2)

        return result
```

### Solution :

Method 1 (Brute Force) :
```go
func largestSquareArea(bottomLeft [][]int, topRight [][]int) int64 {
    var result int64
    n := len(bottomLeft)
    for index1 := 0; index1 < n; index1++ {
        for index2 := index1+1; index2 < n; index2++ {
            length := minimumLength(bottomLeft[index1], bottomLeft[index2], topRight[index1], topRight[index2])
            if length*length > result {
                result = length * length
            }
        }
    }

    return result
}

/* Option 1 */
func minimumLength(bl1 []int, bl2 []int, tr1 []int, tr2 []int) int64 {
/*
Option 2
func minimumLength(bl1, bl2, tr1, tr2 []int) int64 {
*/
    minimum_x := max(bl1[0], bl2[0])
    minimum_y := max(bl1[1], bl2[1])
    maximum_x := min(tr1[0], tr2[0])
    maximum_y := min(tr1[1], tr2[1])

    length := 0
    if minimum_x < maximum_x && minimum_y < maximum_y {
        length = min(maximum_x-minimum_x, maximum_y-minimum_y)
    }

    return int64(length)
}
```
