![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1337. [The K Weakest Rows In A Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix)

### Solution :

Method 1 (Sort) :
```python
class Solution:
    def kWeakestRows(self, mat: List[List[int]], k: int) -> List[int]:
        result = []
        for index, row in enumerate(mat):
            result.append((sum(row), index))

        return [item[1] for item in sorted(result)[:k]]
```

Method 2 (Binary Heap) :
```python
class Solution:
    def kWeakestRows(self, mat: List[List[int]], k: int) -> List[int]:
        min_heap = []
        for index, row in enumerate(mat):
            heapq.heappush(min_heap, (-sum(row), -index))

            if len(min_heap) > k:
                heapq.heappop(min_heap)

        # Option 1
        result = []
        while min_heap:
            _, index = heapq.heappop(min_heap)
            result.append(-index)
        return result[::-1]
        """
        # Option 2
        return [-item[1] for item in sorted(min_heap, reverse=True)]
        """
```

Method 3 (Binary Search + Binary Heap) :
```python
class Solution:
    def kWeakestRows(self, mat: List[List[int]], k: int) -> List[int]:
        min_heap = []
        for index, row in enumerate(mat):
            left = 0
            right = len(row) - 1
            while left <= right:
                middle = left + (right - left)//2
                if row[middle] == 0:
                    right = middle - 1
                else:
                    left = middle + 1
            # `left` is the amount of 1, `right` is the rightest index of 1
            heapq.heappush(min_heap, (-left, -index))

            if len(min_heap) > k:
                heapq.heappop(min_heap)

        return [-item[1] for item in sorted(min_heap, reverse=True)]
```

### Solution :

Method 1 (Sort) :
```php
class Solution {

    /**
     * @param Integer[][] $mat
     * @param Integer $k
     * @return Integer[]
     */
    function kWeakestRows($mat, $k) {
        $soldiers = [];
        foreach($mat as $index => $row) {
            $soldiers[$index] = [array_sum($row), $index];
        }
        sort($soldiers);
        return array_map(function ($item) {
            return $item[1];
        }, array_splice($soldiers, 0, $k));
    }
}
```
