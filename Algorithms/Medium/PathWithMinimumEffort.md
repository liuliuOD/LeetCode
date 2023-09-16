![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1631. [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def minimumEffortPath(self, heights: List[List[int]]) -> int:
        left = 0
        right = max([max(row) for row in heights])
        while left <= right:
            middle = left + (right - left) // 2

            visited = set([(0, 0)])
            if self.dfs(0, 0, middle, visited, heights):
                right = middle - 1
            else:
                left = middle + 1

        return left

    def dfs(self, x, y, threshold, visited, heights) -> bool:
        row = len(heights)
        column = len(heights[0])
        if x == row-1 and y == column-1:
            return True

        for offset_x, offset_y in [[-1, 0], [0, -1], [0, 1], [1, 0]]:
            x_next = x + offset_x
            y_next = y + offset_y
            key = (x_next, y_next)
            if x_next < 0 or x_next >= row or y_next < 0 or y_next >= column or key in visited:
                continue

            cost = abs(heights[x][y] - heights[x_next][y_next])
            if cost > threshold:
                continue

            visited.add(key)
            if self.dfs(x_next, y_next, threshold, visited, heights):
                return True

        return False
```

Method 2 (Dijkstra's Algorithm) :
```python
class Solution:
    def minimumEffortPath(self, heights: List[List[int]]) -> int:
        m = len(heights)
        n = len(heights[0])

        costs = [[float('inf')]*n for _ in range(m)]
        costs[0][0] = 0
        min_heap = [(0, 0, 0)]
        while min_heap:
            cost_previous, x, y = heapq.heappop(min_heap)

            if x == m-1 and y == n-1:
                return cost_previous

            for offset_x, offset_y in [[-1, 0], [0, -1], [0, 1], [1, 0]]:
                x_next = x + offset_x
                y_next = y + offset_y
                if x_next < 0 or x_next >= m or y_next < 0 or y_next >= n:
                    continue

                cost_current = max(cost_previous, abs(heights[x][y]-heights[x_next][y_next]))
                if cost_current >= costs[x_next][y_next]:
                    continue
                costs[x_next][y_next] = cost_current
                heapq.heappush(min_heap, (cost_current, x_next, y_next))
```

### Solution :

Method 1 (Binary Search, Time Complexity: $O(MN*logMN)$) :
```php
class Solution {

    /**
     * @param Integer[][] $heights
     * @return Integer
     */
    function minimumEffortPath($heights) {
        $left = 0;
        $right = array_reduce($heights, function ($a, $b) {
            return max($a, max($b));
        }, 0);

        while ($left <= $right) {
            $middle = $left + intval(($right - $left) / 2);

            $visited = ["0-0" => true];
            if ($this->dfs($middle, 0, 0, $visited, $heights)) {
                $right = $middle - 1;
            } else {
                $left = $middle + 1;
            }
        }

        return $left;
    }

    function dfs($costThreshold, $x, $y, &$visited, $heights) {
        $row = count($heights);
        $column = count($heights[0]);

        if ($x == $row-1 && $y == $column-1) {
            return true;
        }

        foreach([[-1, 0], [0, -1], [0, 1], [1, 0]] as [$offsetX, $offsetY]) {
            $xNext = $x + $offsetX;
            $yNext = $y + $offsetY;
            $key = "$xNext-$yNext";
            if ($xNext < 0 || $xNext >= $row || $yNext < 0 || $yNext >= $column || isset($visited[$key])) {
                continue;
            }

            $cost = abs($heights[$x][$y] - $heights[$xNext][$yNext]);
            if ($cost > $costThreshold) {
                continue;
            }

            $visited[$key] = true;
            if ($this->dfs($costThreshold, $xNext, $yNext, $visited, $heights)) {
                return true;
            }
        }

        return false;
    }
}
```

Method 2 (Dijkstra's Algorithm) :
```php
class Solution {

    /**
     * @param Integer[][] $heights
     * @return Integer
     */
    function minimumEffortPath($heights) {
        $row = count($heights);
        $column = count($heights[0]);

        $costs = array_fill(0, $row, array_fill(0, $column, PHP_INT_MAX));
        $costs[0][0] = 0;

        $minHeap = new SplMinHeap();
        $minHeap->insert([0, [0, 0]]);
        while ($minHeap->count()) {
            list($costPrevious, list($x, $y)) = $minHeap->extract();

            if ($x == $row-1 && $y == $column-1) {
                return $costPrevious;
            }

            foreach([[-1, 0], [0, -1], [0, 1], [1, 0]] as list($offsetX, $offsetY)) {
                $xNext = $x + $offsetX;
                $yNext = $y + $offsetY;
                if ($xNext < 0 || $xNext >= $row || $yNext < 0 || $yNext >= $column) {
                    continue;
                }

                $costCurrent = max($costPrevious, abs($heights[$x][$y] - $heights[$xNext][$yNext]));
                if ($costCurrent >= $costs[$xNext][$yNext]) {
                    continue;
                }

                $costs[$xNext][$yNext] = $costCurrent;
                $minHeap->insert([$costCurrent, [$xNext, $yNext]]);
            }
        }
    }
}
```
