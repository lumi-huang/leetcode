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

### 633. Sum of Square Numbers
```python
class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        a = 0
        b = int(math.sqrt(c))
        while a<=b:
            squaresum = a*a + b*b
            if squaresum == c:
                return True
            elif squaresum < c:
                a += 1
            else:
                b -= 1
        return False
```


### 345. Reverse Vowels of a String
```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = 'aeiouAEIOU'
        i = 0
        j = len(s)-1
        s = list(s)
        while i < j:
            if s[i] in vowels and s[j] in vowels:
                s[i], s[j] = s[j], s[i]
                i+=1
                j-=1
            elif s[i] in vowels and s[j] not in vowels:
                j -= 1
            elif s[j] in vowels and s[i] not in vowels:
                i += 1
            else:
                i+=1
                j-=1
        return(''.join(s))                
```

### 680. Valid Palindrome II
```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        i, j = 0, len(s)-1
        while i <= j:
            if s[i] == s[j]:
                i += 1
                j -= 1
            else:
                return(s[i+1:j+1] == s[i+1:j+1][::-1] or s[i:j] == s[i:j][::-1])
        return True

```

### 88. Merge Sorted Array
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i = m-1
        j = n-1
        k = m+n-1
        while j >= 0:
            if(i<0 or nums1[i] <= nums2[j]):
                nums1[k] = nums2[j]
                j -= 1
            else:
                nums1[k] = nums1[i]
                i -= 1
            k -= 1
                
        
        return(nums1)
```

### 141. Linked List Cycle
```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if head is None or head.next is None:
            return False
        slow = head
        fast = head.next
        while(slow != fast):
            if fast is None or fast.next is None:
                return False
            fast = fast.next.next
            slow = slow.next
        return True
```
