![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 135. [Candy](https://leetcode.com/problems/candy)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 44/48) :
```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        candies = [1] * n
        sum_candies = 0
        while True:
            for index in range(n):
                index_previous = index - 1
                if index_previous >= 0 and ratings[index] > ratings[index_previous]:
                    candies[index] = max(candies[index], candies[index_previous]+1)

                index_next = index + 1
                if index_next < n and ratings[index] > ratings[index_next]:
                    candies[index] = max(candies[index], candies[index_next]+1)

            if sum(candies) == sum_candies:
                break

            sum_candies = sum(candies)

        return sum_candies
```

Method 2 (Greedy) :
```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        candies = [1] * n
        for index in range(n):
            self.give_candies(index, candies, ratings)

        for index in reversed(range(n)):
            self.give_candies(index, candies, ratings)

        return sum(candies)

    def give_candies(self, index_current: int, candies: List[int], ratings: List[int]):
        n = len(ratings)
        index_previous = index_current - 1
        if index_previous >= 0 and ratings[index_current] > ratings[index_previous]:
            candies[index_current] = candies[index_previous] + 1

        index_next = index_current + 1
        if index_next < n and ratings[index_current] > ratings[index_next]:
            candies[index_current] = max(candies[index_current], candies[index_next]+1)
```

Method 3 (Greedy) :
```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        candies = [1] * n

        for index in range(1, n):
            index_previous = index - 1
            if ratings[index] > ratings[index_previous]:
                candies[index] = candies[index_previous] + 1

        for index in reversed(range(n-1)):
            index_next = index + 1
            if ratings[index] > ratings[index_next]:
                candies[index] = max(candies[index], candies[index_next]+1)

        return sum(candies)
```

### Solution :

Method 1 (Greedy) :
```php
class Solution {

    /**
     * @param Integer[] $ratings
     * @return Integer
     */
    function candy($ratings) {
        $n = count($ratings);
        $candies = array_fill(0, $n, 1);

        for ($index = 1; $index < $n; $index++) {
            $indexPrevious = $index - 1;
            if ($ratings[$indexPrevious] < $ratings[$index]) {
                $candies[$index] = $candies[$indexPrevious] + 1;
            }
        }

        for ($index = $n-2; $index >= 0; $index--) {
            $indexNext = $index + 1;
            if ($ratings[$indexNext] < $ratings[$index]) {
                $candies[$index] = max($candies[$index], $candies[$indexNext]+1);
            }
        }

        return array_sum($candies);
    }
}
```
