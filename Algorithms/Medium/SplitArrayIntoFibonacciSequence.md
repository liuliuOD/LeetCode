![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 842. [Split Array Into Fibonacci Sequence](https://leetcode.com/problems/split-array-into-fibonacci-sequence)

### Solution :

Method 1 (Backtracking) :
```python
MAXIMUM = 2**31
class Solution:
    def splitIntoFibonacci(self, num: str) -> List[int]:
        memoization = []
        self.backtracking(0, memoization, num)
        return memoization

    def backtracking(self, index: int, memoization: List[int], num: str) -> bool:
        n = len(num)

        if index == n and len(memoization) > 2:
            return True

        for index_tail in range(index+1, n+1):
            if num[index] == '0' and index_tail > index+1:
                break

            current = int(num[index:index_tail])
            if current >= MAXIMUM:
                break

            amount = len(memoization)
            # amount >= 2 means there are 3 items when including current item
            if amount >= 2:
                sum_of_previous_2 = memoization[amount-1] + memoization[amount-2]
                if current > sum_of_previous_2:
                    break
                elif current < sum_of_previous_2:
                    continue

            memoization.append(current)
            if self.backtracking(index_tail, memoization, num):
                return True
            memoization.pop()

        return False
```

### Solution :

Method 1 (Backtracking) :
```php
class Solution {

    /**
     * @param String $num
     * @return Integer[]
     */
    function splitIntoFibonacci($num) {
        $this->MAXIMUM = pow(2, 31);
        $memoization = [];
        $this->backtracking(0, $memoization, $num);
        return $memoization;
    }

    function backtracking($index, &$memoization, $num) {
        $n = strlen($num);

        if ($index == $n && count($memoization) > 2) {
            return true;
        }

        for ($indexNext = $index; $indexNext < $n; $indexNext++) {
            // can't use zero-headed like '01'
            if ($num[$index] === '0' && $indexNext > $index) {
                break;
            }

            $amount = count($memoization);
            $current = intval(substr($num, $index, $indexNext-$index+1));
            $sum2Previous = $memoization[$amount-1] + $memoization[$amount-2];
            if ($current >= $this->MAXIMUM) {
                break;
            }

            if ($amount >= 2) {
                if ($current > $sum2Previous) {
                    break;
                } else if ($current < $sum2Previous) {
                    continue;
                }
            }

            // not use array_push to reduce the cost of function call
            $memoization[] = $current;
            if ($this->backtracking($indexNext+1, $memoization, $num)) {
                return true;
            }
            array_pop($memoization);
        }
        return false;
    }
}
```
