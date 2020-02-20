### 215. Kth Largest Element in an Array

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return(sorted(nums)[-k])
```

### 347. Top K Frequent Elements
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        freq = {}
        for i in nums:
            if i in freq:
                freq[i] += 1
            else:
                freq[i] = 1
        sorted_freq = dict(sorted(freq.items(), key=operator.itemgetter(1),reverse=True))
        return(list(sorted_freq.keys())[0:k])
```

### 451. Sort Characters By Frequency

counter solution
```python
class Solution:
    def frequencySort(self, s: str) -> str:
        return("".join(c*n for c, n in collections.Counter(s).most_common()))
```

dict solution
```python
class Solution:
    def frequencySort(self, s: str) -> str:
        hmap = {}
        for char in list(s):
            if char not in hmap:
                hmap[char] = 1
            else:
                hmap[char] += 1
        
        return("".join(c*n for c, n in sorted(hmap.items(), key=operator.itemgetter(1), reverse=True)))
```

### 75. Sort Colors
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        for i in range(len(nums)):
            min_ind = i
            for j in range(i+1, len(nums)):
                if nums[j] < nums[min_ind]:
                    min_ind = j
            nums[i], nums[min_ind] = nums[min_ind], nums[i]
        return nums
    
```
