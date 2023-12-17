![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2353. [Design A Food Rating System](https://leetcode.com/problems/design-a-food-rating-system)

### Solution :

```python
# Your FoodRatings object will be instantiated and called as such:
# obj = FoodRatings(foods, cuisines, ratings)
# obj.changeRating(food,newRating)
# param_2 = obj.highestRated(cuisine)
```

Method 1 (Hash Map) :
```python
class FoodRatings:

    def __init__(self, foods: List[str], cuisines: List[str], ratings: List[int]):
        n = len(foods)
        self.food_name_order: Dict[str, int] = {}
        self.food_order_name = []
        for index, food_name in enumerate(sorted(foods, reverse=True)):
            self.food_name_order[food_name] = index
            self.food_order_name.append(food_name)

        self.items: List[Tuple[str, int]] = [() for _ in range(n)]
        self.rates: Dict[str, List[Tuple[int, int]]] = defaultdict(list)
        for index, food_name in enumerate(foods):
            food_order = self.food_name_order[food_name]
            food_type = cuisines[index]
            food_rate = ratings[index]
            self.items[food_order] = (food_type, food_rate)
            self.rates[food_type].append((food_rate, food_order))

        for key in self.rates.keys():
            self.rates[key].sort()

    def changeRating(self, food_name: str, rating_new: int) -> None:
        food_order = self.food_name_order[food_name]
        food_type, food_rate = self.items[food_order]
        self.items[food_order] = (food_type, rating_new)
        index_old = bisect.bisect_left(self.rates[food_type], (food_rate, food_order))
        self.rates[food_type].pop(index_old)

        food_new = (rating_new, food_order)
        index_new = bisect.bisect(self.rates[food_type], food_new)
        self.rates[food_type].insert(index_new, food_new)

    def highestRated(self, cuisine: str) -> str:
        return self.food_order_name[self.rates[cuisine][-1][1]]
```
