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
