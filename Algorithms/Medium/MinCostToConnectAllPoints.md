![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1584. [Min Cost To Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points)

### Solution :

Method 1 (Kruskal's Algorithm) :
```php
class UnionSet {
    function __construct($n) {
        $this->cost = 0;
        $this->amountEdges = 0;

        $this->points = array_fill(0, $n, 0);
        for ($index = 0; $index < $n; $index++) {
            $this->points[$index] = $index;
        }
    }

    function find($point) {
        if ($this->points[$point] != $point) {
            $this->points[$point] = $this->find($this->points[$point]);
        }

        return $this->points[$point];
    }

    function union($pointA, $pointB, $cost) {
        $parentA = $this->find($pointA);
        $parentB = $this->find($pointB);

        if ($parentA != $parentB) {
            $this->points[$parentA] = $parentB;
            $this->amountEdges++;
            $this->cost += $cost;
        }

        return $this->amountEdges;
    }
}

class Solution {

    /**
     * @param Integer[][] $points
     * @return Integer
     */
    function minCostConnectPoints($points) {
        $n = count($points);
        $edges = [];
        for ($indexStart = 0; $indexStart < $n; $indexStart++) {
            for ($indexEnd = $indexStart+1; $indexEnd < $n; $indexEnd++) {
                $edges[] = [abs($points[$indexEnd][0] - $points[$indexStart][0]) + abs($points[$indexEnd][1] - $points[$indexStart][1]), $indexStart, $indexEnd];
            }
        }
        sort($edges);

        $unionSet = new UnionSet($n);
        foreach ($edges as [$cost, $indexStart, $indexEnd]) {
            if ($unionSet->union($indexStart, $indexEnd, $cost) == $n-1) {
                break;
            }
        }

        return $unionSet->cost;
    }
}
```

Method 2 (Prim's Algorithm) :
```php
class Solution {

    /**
     * @param Integer[][] $points
     * @return Integer
     */
    function minCostConnectPoints($points) {
        $n = count($points);

        $minHeap = new SplMinHeap();
        $minHeap->insert([0, 0]);
        $visited = [];
        $distances = [0 => 0];
        $result = 0;
        while ($minHeap->count()) {
            list($cost, $indexPoint) = $minHeap->extract();

            if (in_array($indexPoint, $visited) || (isset($distance[$indexPoint]) && $distance[$indexPoint] <= $cost)) {
                continue;
            }
            $visited[] = $indexPoint;

            $result += $cost;

            for ($index = 0; $index < $n; $index++) {
                if (in_array($index, $visited)) {
                    continue;
                }

                $distance = $this->getDistance($points[$index], $points[$indexPoint]);
                if (isset($distances[$key]) && $distances[$index] <= $distance) {
                    continue;
                }

                $distances[$index] = $distance;
                $minHeap->insert([$distance, $index]);
            }
        }

        return $result;
    }

    function getDistance(Array $pointStart, Array $pointEnd) : Int {
        return abs($pointStart[0] - $pointEnd[0]) + abs($pointStart[1] - $pointEnd[1]);
    }
}
```
