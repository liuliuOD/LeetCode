![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1603. [Design Parking System](https://leetcode.com/problems/remove-trailing-zeros-from-a-string)

### Solution :

```rust
/**
 * Your ParkingSystem object will be instantiated and called as such:
 * let obj = ParkingSystem::new(big, medium, small);
 * let ret_1: bool = obj.add_car(carType);
 */
```

Method 1 :
```rust
use std::collections::HashMap;
struct ParkingSystem {
    parking_info: HashMap<i32, Vec<i32>>
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl ParkingSystem {

    fn new(big: i32, medium: i32, small: i32) -> Self {
        let mut map = HashMap::new();
        map.insert(1, vec![big, 0]);
        map.insert(2, vec![medium, 0]);
        map.insert(3, vec![small, 0]);
        Self {
            parking_info: map
        }
    }
    
    fn add_car(&mut self, car_type: i32) -> bool {
        if !self.parking_info.contains_key(&car_type) {
            return false
        }

        if self.parking_info[&car_type][0] == self.parking_info[&car_type][1] {
            return false
        }

        self.parking_info.entry(car_type).and_modify(|vec| vec[1] += 1);
        return true
    }
}
```

### Solution :

```python
# Your ParkingSystem object will be instantiated and called as such:
# obj = ParkingSystem(big, medium, small)
# param_1 = obj.addCar(carType)
```

Method 1 (In weekly contest 347, regular expression) :
```python
class ParkingSystem:

    def __init__(self, big: int, medium: int, small: int):
        self.parking_space = {
            1: [big, 0],
            2: [medium, 0],
            3: [small, 0]
        }

    def addCar(self, carType: int) -> bool:
        if carType not in self.parking_space:
            return False

        [space, used] = self.parking_space[carType]
        if space == used:
            return False

        self.parking_space[carType][1] += 1
        return True
```
