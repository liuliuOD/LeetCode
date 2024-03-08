![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 338. [Counting Bits](https://leetcode.com/problems/counting-bits)

### Solution :

Method 1 (DFS) :
```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        result = []
        for value in range(n+1):
            result.append(self.dfs(value))
        return result
        
    def dfs(self, value: int) -> int:
        if value <= 1:
            return value
        
        if value % 2 == 0:
            return self.dfs(value // 2)
        else:
            return 1 + self.dfs(value // 2)
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        self.memoization = {0: 0, 1: 1}
        result = []
        for value in range(n+1):
            result.append(self.dfs(value))
        return result
        
    def dfs(self, value: int) -> int:
        if value in self.memoization:
            return self.memoization[value]
        
        next_value = value // 2
        if value % 2 == 0:
            self.memoization[value] = self.dfs(next_value)
        else:
            self.memoization[value] = 1 + self.dfs(next_value)
        
        return self.memoization[value]
```

Method 3 (Dynamic Programming) :
```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        self.memoization = {0: 0, 1: 1}
        result = []
        for value in range(n+1):
            result.append(self.dfs(value))
        return result
        
    def dfs(self, value: int) -> int:
        if value in self.memoization:
            return self.memoization[value]
        
        next_value = value // 2
        self.memoization[value] = self.dfs(next_value)
        if value % 2 == 1:
            self.memoization[value] += 1
        
        return self.memoization[value]
```

Method 4 (Dynamic Programming):
```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        self.memoization = {0: 0, 1: 1}
        result = []
        for value in range(n+1):
            result.append(self.dfs(value))
        return result

    def dfs(self, value: int) -> int:
        if value in self.memoization:
            return self.memoization[value]

        # bitwise right side move, if first bit is 1 then need to record in memoization to save the amount of number 1
        self.memoization[value] = value % 2 + self.dfs(value >> 1)

        return self.memoization[value]
```

### Solution :

Method 1 (Brute Force) :
```php
class Solution {

    /**
     * @param Integer $n
     * @return Integer[]
     */
    function countBits($n) {
        $result = [];
        for ($num=0; $num <= $n; $num++) {
            $amount = 0;
            $temp = $num;
            while ($temp) {
                $amount += intval($temp & 1);
                $temp = $temp >> 1;
            }
            $result[] = $amount;
        }

        return $result;
    }
}
```

Method 2 (Dynamic Programming) :
```php
class Solution {

    /**
     * @param Integer $n
     * @return Integer[]
     */
    function countBits($n) {
        $memoization = [];
        $result = [];
        for ($num=0; $num <= $n; $num++) {
            $amount = 0;
            $temp = $num;
            while ($temp) {
                if (isset($memoization[$temp])) {
                    $amount += $memoization[$temp];
                    break;
                }

                $amount += intval($temp & 1);
                $temp = $temp >> 1;
            }

            $memoization[$temp] = $amount;
            $result[] = $amount;
        }

        return $result;
    }
}
```
