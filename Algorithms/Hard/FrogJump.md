![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 403. [Frog Jump](https://leetcode.com/problems/frog-jump)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def canCross(self, stones: List[int]) -> bool:
        memoization = defaultdict(lambda: defaultdict(bool))

        return self.dfs(0, memoization, stones[0], stones[-1], set(stones))

    def dfs(self, jump: int, memoization: Dict[int, Dict[int, bool]], current: int, target: int, stones: Set[int]) -> bool:
        if current == target:
            return True

        if jump in memoization[current]:
            return memoization[current][jump]

        result = False
        for offset in [-1, 0, 1]:
            jump_next = jump + offset
            next_stone = current + jump_next
            if next_stone not in stones or jump_next <= 0:
                continue

            result |= self.dfs(jump_next, memoization, next_stone, target, stones)

        memoization[current][jump] = result
        return result
```

Method 2 (Dynamic Programming, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def canCross(self, stones: List[int]) -> bool:
        dp: Dict[int, Dict[int, bool]] = defaultdict(lambda: defaultdict(bool))
        dp[0][1] = True # [index_stone][jump]
        for index_current, stone_current in enumerate(stones):
            for index_previous in range(index_current):
                stone_previous = stones[index_previous]
                jump = stone_current - stone_previous

                if jump <= index_previous+1:
                    dp[index_current][jump] = dp[index_previous][jump-1] or dp[index_previous][jump] or dp[index_previous][jump+1]

                if index_current == len(stones)-1 and dp[index_current][jump]:
                    return True

        return False
```

### Solution :

Method 1 (DFS + Memoization) :
```php
class Solution {

    /**
     * @param Integer[] $stones
     * @return Boolean
     */
    function canCross($stones) {
        $this->memoization = [];

        return $this->dfs(0, $stones[0], $stones);
    }

    function dfs(int $jump, int $currentStone, array $stones) : bool {
        if ($currentStone === $stones[count($stones)-1]) {
            return true;
        }

        $key = sprintf('%d-%d', $currentStone, $jump);
        if (isset($this->memoization[$key])) {
            return $this->memoization[$key];
        }

        $result = false;
        foreach([-1, 0, 1] as $offset) {
            $jumpNext = $jump + $offset;
            $nextStone = $currentStone + $jumpNext;
            if ($jumpNext <= 0 || !in_array($nextStone, $stones)) {
                continue;
            }

            $result |= $this->dfs($jumpNext, $nextStone, $stones);
        }

        return $this->memoization[$key] = $result;
    }
}
```
