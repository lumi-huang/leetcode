### 215. Kth Largest Element in an Array

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return(sorted(nums)[-k])
```

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        for j in range(1, len(nums)):
            key = nums[j]
            i = j-1
            while i>=0 and nums[i] > key:
                nums[i+1] = nums[i]
                i = i-1
            nums[i+1] = key
        
        return(nums[-k])
```

### 347. Top K Frequent Elements
```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        c = collections.Counter(nums).most_common(k)
        key = []
        for k, v in c:
            key.append(k)
        return(key)
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
