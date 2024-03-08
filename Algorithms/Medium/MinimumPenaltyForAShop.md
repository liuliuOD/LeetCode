![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2483. [Minimum Penalty For A Shop](https://leetcode.com/problems/minimum-penalty-for-a-shop)

### Solution :

Method 1 (Greedy, right to left, Time Complexity: $O(N)$) :
```python
class Solution:
    def bestClosingTime(self, customers: str) -> int:
        penalty_current = 0
        for customer in customers:
            if customer == 'N':
                penalty_current += 1

        penalty_minimum = penalty_current
        result = pointer = len(customers)
        while pointer > 0:
            pointer -= 1
            if customers[pointer] == 'Y':
                penalty_current += 1
            elif customers[pointer] == 'N':
                penalty_current -= 1

            if penalty_current <= penalty_minimum:
                result = pointer
                penalty_minimum = penalty_current

        return result
```

### Solution :

Method 1 (Greedy, left to right, Time Complexity: $O(N)$) :
```php
class Solution {

    /**
     * @param String $customers
     * @return Integer
     */
    function bestClosingTime($customers) {
        $penalty = 0;
        $customers = str_split($customers);
        foreach ($customers as $char) {
            if ($char == 'Y') {
                $penalty++;
            }
        }
        $n = count($customers);

        $result = $n;
        $pointer = 0;
        $penaltyMinimum = INF;
        while ($pointer <= $n) {
            if ($pointer > 0) {
                if ($customers[$pointer-1] == 'Y')
                    $penalty--;
                else if ($customers[$pointer-1] == 'N')
                    $penalty++;
            }

            if ($penaltyMinimum > $penalty) {
                $result = $pointer;
                $penaltyMinimum = $penalty;
            }

            $pointer++;
        }

        return $result;
    }
}
```
