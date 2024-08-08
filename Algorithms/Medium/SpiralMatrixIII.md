![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 885. [Spiral Matrix III](https://leetcode.com/problems/spiral-matrix-iii)

### Solution :

Method 1 (Simulation, Time Complexity: $O(MAX(M, N)^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def spiralMatrixIII(self, rows: int, cols: int, r_start: int, c_start: int) -> List[List[int]]:
        r_current, c_current = r_start, c_start
        result = [(r_current, c_current)]
        for step in range(1, max(r_start, rows+1-r_start, c_start, cols+1-c_start)*2+1+1):
            if step % 2 == 1:
                # right and down
                for _ in range(1, step+1):
                    c_current += 1
                    if 0<= r_current < rows and 0 <= c_current < cols:
                        result.append((r_current, c_current))

                for _ in range(1, step+1):
                    r_current += 1
                    if 0 <= r_current < rows and 0 <= c_current < cols:
                        result.append((r_current, c_current))
            else:
                # left and top
                for _ in range(1, step+1):
                    c_current -= 1
                    if 0 <= r_current < rows and 0 <= c_current < cols:
                        result.append((r_current, c_current))

                for _ in range(1, step+1):
                    r_current -= 1
                    if 0 <= r_current < rows and 0 <= c_current < cols:
                        result.append((r_current, c_current))

        return result
```

Method 2 (Simulation, Time Complexity: $O(MAX(M, N)^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def spiralMatrixIII(self, rows: int, cols: int, r_start: int, c_start: int) -> List[List[int]]:
        r_current, c_current = r_start, c_start
        direction = 0
        result = [(r_current, c_current)]
        for step in range(1, max(r_start, rows+1-r_start, c_start, cols+1-c_start)*2+1+1):
            # right -> down -> left -> top
            for _ in range(2):
                for _ in range(step):
                    match direction:
                        case 0:
                            c_current += 1
                        case 1:
                            r_current += 1
                        case 2:
                            c_current -= 1
                        case 3:
                            r_current -= 1

                    if 0 <= r_current < rows and 0 <= c_current < cols:
                        result.append((r_current, c_current))

                direction = (direction + 1) % 4

        return result
```
