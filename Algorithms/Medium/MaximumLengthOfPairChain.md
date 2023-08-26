![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 646. [Maximum Length Of Pair Chain](https://leetcode.com/problems/maximum-length-of-pair-chain)

### Solution :

Method 1 (DFS + Memoization) :
```python
class Solution:
    def findLongestChain(self, pairs: List[List[int]]) -> int:
        self.result = 0
        pairs.sort(key=lambda x: x[1])

        memoization = defaultdict(int)
        return self.dfs(0, 0, [-1001, -1001], memoization, pairs)

    def dfs(self, longest_chain: int, index: int, pair_previous: List[int], memoization: Dict[Tuple[int], int], pairs: List[List[int]]) -> int:
        if index >= len(pairs):
            self.result = max(self.result, longest_chain)
            return self.result

        if longest_chain < memoization[(*pair_previous,)]:
            return memoization[(*pair_previous,)]

        longest = 0
        if pair_previous[1] < pairs[index][0]:
            longest = self.dfs(longest_chain+1, index+1, pairs[index], memoization, pairs)
        longest = max(longest, self.dfs(longest_chain, index+1, pair_previous, memoization, pairs))

        memoization[(*pair_previous,)] = longest
        return longest
```

Method 2 (Greedy, Time Complexity: $O(N*logN)$) :
```python
class Solution:
    def findLongestChain(self, pairs: List[List[int]]) -> int:
        result = 0
        current = float('-inf')
        pairs.sort(key=lambda x: x[1])

        for pair_left, pair_right in pairs:
            if pair_left <= current:
                continue

            current = pair_right
            result += 1

        return result
```

Method 3 (Dynamic Programming, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def findLongestChain(self, pairs: List[List[int]]) -> int:
        n = len(pairs)
        dp = [1] * n
        pairs.sort()
        for index in range(n):
            maximum = 1
            for index_previous in range(index):
                if pairs[index_previous][1] < pairs[index][0]:
                    maximum = max(maximum, dp[index_previous]+1)
            dp[index] = maximum

        return max(dp)
```

### Solution :

Method 1 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param Integer[][] $pairs
     * @return Integer
     */
    function findLongestChain($pairs) {
        usort($pairs, function ($left, $right) {
            return $left[0] <=> $right[0];
        });

        $n = count($pairs);
        $dp = array_fill(0, $n, 1);
        foreach ($pairs as $index => $pair) {
            $maximum = 1;
            for ($indexPrevious=0; $indexPrevious < $index; $indexPrevious++) {
                if ($pairs[$indexPrevious][1] < $pair[0]) {
                    $maximum = max($maximum, $dp[$indexPrevious]+1);
                }
            }

            $dp[$index] = $maximum;
        }
        return max($dp);
    }
}
```

Method 2 (Greedy, sort by pair right with ascending order) :
```php
class Solution {

    /**
     * @param Integer[][] $pairs
     * @return Integer
     */
    function findLongestChain($pairs) {
        usort($pairs, function ($left, $right) {
            return $left[1] <=> $right[1];
        });

        $current = -1001;
        $result = 0;
        foreach ($pairs as $pair) {
            if ($pair[0] > $current) {
                $current = $pair[1];
                $result++;
            }
        }

        return $result;
    }
}
```

Method 3 (Greedy, sort by pair left with descending order) :
```php
class Solution {

    /**
     * @param Integer[][] $pairs
     * @return Integer
     */
    function findLongestChain($pairs) {
        // descending
        usort($pairs, function ($left, $right) {
            if ($left[0] == $right[0]) {
                return 0;
            }

            return $left[0] < $right[0]
                ? 1
                : -1;
        });

        $current = 1001;
        $result = 0;
        foreach ($pairs as $pair) {
            if ($pair[1] < $current) {
                $current = $pair[0];
                $result++;
            }
        }

        return $result;
    }
}
```
