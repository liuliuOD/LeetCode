![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 846. [Hand Of Straights](https://leetcode.com/problems/hand-of-straights)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N*Log(N))$ (N: length of `hand`), Space Complexity: $O(N)$) :
```python
class Solution:
    def isNStraightHand(self, hand: List[int], group_size: int) -> bool:
        counter = Counter(hand)
        nums = list(set(counter.keys()))
        nums.sort(reverse=True)
        while nums:
            num_current = nums.pop()
            amount = counter[num_current]
            for offset in range(1, group_size):
                num_next = num_current + offset

                if counter[num_next] < amount:
                    return False
                elif counter[num_next] == amount:
                    if num_next != nums[-1]:
                        return False

                    del counter[num_next]
                    nums.pop()
                else:
                    counter[num_next] -= amount

        return True
```
