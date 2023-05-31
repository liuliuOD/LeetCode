![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1396. [Design Underground System](https://leetcode.com/problems/design-underground-system)

### Solution :

```python
# Your UndergroundSystem object will be instantiated and called as such:
# obj = UndergroundSystem()
# obj.checkIn(id,stationName,t)
# obj.checkOut(id,stationName,t)
# param_3 = obj.getAverageTime(startStation,endStation)
```

Method 1 (Space traded for time) :
```python
class UndergroundSystem:

    def __init__(self):
        self.map = defaultdict(list)
        self.checkInInfo = {}

    def checkIn(self, id: int, stationName: str, t: int) -> None:
        self.checkInInfo[id] = [stationName, t]

    def checkOut(self, id: int, stationName: str, t: int) -> None:
        if id in self.checkInInfo:
            startStation, startTime = self.checkInInfo[id]
            key = self.getMapKey(startStation, stationName)
            self.map[key].append(t - startTime)

            del self.checkInInfo[id]

    def getAverageTime(self, startStation: str, endStation: str) -> float:
        key = self.getMapKey(startStation, endStation)
        return sum(self.map[key]) / len(self.map[key])
    
    def getMapKey(self, startStation: str, endStation: str) -> str:
        return f'{startStation}-{endStation}'
```
