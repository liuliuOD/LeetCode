![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 767. [Reorganize String](https://leetcode.com/problems/reorganize-string)

### Solution :

Method 1 (Backtracking, ERROR: "Time Limit Exceeded", 32/70) :
```python
class Solution:
    def reorganizeString(self, s: str) -> str:
        self.result = ''
        mapping = defaultdict(int)
        for ch in s:
            mapping[ch] += 1

        self.backtracking(mapping)
        return self.result

    def backtracking(self, mapping: Dict[str, int]) -> bool:
        if sum(mapping.values()) == 0:
            return True

        for ch, amount in mapping.items():
            if amount <= 0 or (self.result and self.result[-1] == ch):
                continue

            mapping[ch] -= 1
            self.result += ch
            if self.backtracking(mapping):
                return True
            self.result = self.result[:-1]
            mapping[ch] += 1

        return False
```

Method 2 (Max Heap) :
```python
class Solution:
    def reorganizeString(self, s: str) -> str:
        mapping = defaultdict(int)
        for ch in s:
            mapping[ch] += 1

        result = ''
        max_heap = [(-amount, key) for key, amount in mapping.items()]
        heapq.heapify(max_heap)
        while len(max_heap) > 1:
            top_1, top_2 = heapq.heappop(max_heap), heapq.heappop(max_heap)
            result += top_1[1] + top_2[1]

            if top_1[0]+1 < 0:
                heapq.heappush(max_heap, (top_1[0]+1, top_1[1]))
            if top_2[0]+1 < 0:
                heapq.heappush(max_heap, (top_2[0]+1, top_2[1]))

        if len(max_heap) == 0:
            return result

        last_item = max_heap[0]
        return result + last_item[1] if -last_item[0] == 1 else ''
```

### Solution :

Method 1 (Max Heap) :
```php
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function reorganizeString($s) {
        $mapping = [];
        foreach (str_split($s) as $char) {
            isset($mapping[$char])
                ? $mapping[$char] += 1
                : $mapping[$char] = 1;
        }

        $maxHeap = new SplMaxHeap();
        foreach ($mapping as $key => $amount) {
            $maxHeap->insert([$amount, $key]);
        }

        $result = [];
        while (count($maxHeap) > 1) {
            [$top1Value, $top1Key] = $maxHeap->extract();
            [$top2Value, $top2Key] = $maxHeap->extract();

            $top1Value--;
            $top2Value--;

            $result[] = $top1Key;
            $result[] = $top2Key;

            if ($top1Value > 0) {
                $maxHeap->insert([$top1Value, $top1Key]);
            }
            if ($top2Value > 0) {
                $maxHeap->insert([$top2Value, $top2Key]);
            }
        }

        if (count($maxHeap)) {
            [$remainValue, $remainKey] = $maxHeap->extract();

            if ($remainValue > 1 || $remainKey == $result[count($result)-1]) {
                return '';
            }

            $result[] = $remainKey;
        }

        return implode('', $result);
    }
}
```
