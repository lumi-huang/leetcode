### 167. Two Sum II - Input array is sorted

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        index1 = 0
        index2 = len(numbers)-1
        total = numbers[index1] + numbers[index2]
        while total != target:
            if total < target:
                index1 += 1
            if total > target:
                index2 -= 1
            total = numbers[index1] + numbers[index2]
        return [index1+1, index2+1]
```
