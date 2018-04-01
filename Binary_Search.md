# Binary Search @ lintcode

457. Classical Binary Search
```python
class Solution:
    """
    @param: nums: An integer array sorted in ascending order
    @param: target: An integer
    @return: An integer
    """
    def findPosition(self, nums, target):
        # write your code here
        # Corner cases
        if not nums or len(nums) == 0:
            return -1
        
        start = 0
        end = len(nums) - 1
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                start = mid
            elif nums[mid] > target:
                end = mid
        
        if nums[start] == target:
            return start
        if nums[end] == target:
            return end
        else:
            return -1

```
14. First Position of Target 
```python
class Solution:
    """
    @param nums: The integer array.
    @param target: Target to find.
    @return: The first position of target. Position starts from 0.
    """
    def binarySearch(self, nums, target):
        # write your code here
        # Corner cases
        if not nums or len(nums) == 0:
            return -1
        
        start = 0
        end = len(nums) - 1
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if nums[mid] == target:
                end = mid # first one must be on the left
            elif nums[mid] < target:
                start = mid
            elif nums[mid] > target:
                end = mid
        
        if nums[start] == target:
            return start
        if nums[end] == target:
            return end
        else:
            return -1
```
458. Last Position of Target
```python
class Solution:
    """
    @param nums: An integer array sorted in ascending order
    @param target: An integer
    @return: An integer
    """
    def lastPosition(self, nums, target):
        # write your code here
        # Corner cases
        if not nums or len(nums) == 0:
            return -1
            
        start = 0
        end = len(nums) - 1
        
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if nums[mid] == target:
                start = mid # last one if in the right part
            elif nums[mid] < target:
                start = mid
            elif nums[mid] > target:
                end = mid
 
        if nums[end] == target:
            return end       
        elif nums[start] == target:
            return start
        else:
            return -1

```
585. Maximum Number in Mountain Sequence
```python
class Solution:
    """
    @param nums: a mountain sequence which increase firstly and then decrease
    @return: then mountain top
    """
    def mountainSequence(self, nums):
        # write your code here
        if not nums or len(nums) == 0:
            return -1
        
        start = 0
        end = len(nums) - 1
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if nums[mid] < nums[mid + 1]:
                start = mid
            elif nums[mid] > nums[mid + 1]:
                end = mid
        
        return max(nums[start], nums[end]) # trick
```
447. Search in a Big Sorted Array
```python
class Solution:
    """
    @param: reader: An instance of ArrayReader.
    @param: target: An integer
    @return: An integer which is the first index of target.
    """
    def searchBigSortedArray(self, reader, target):
        # write your code here
        # find the left limit
        index = 1 # if index = 0, index * 2 ==0
        while(reader.get(index - 1) < target):
            index = index * 2
        # find the target in [0, left limit]
        start = 0
        end = index - 1
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if reader.get(mid) == target:
                end = mid
            if reader.get(mid) < target:
                start = mid
            elif reader.get(mid) > target:
                end = mid
        
        if reader.get(start) == target:
            return start
        elif reader.get(end) == target:
            return end
        else:
            return -1
```
159. Find Minimum in Rotated Sorted Array
```python
class Solution:
    """
    @param nums: a rotated sorted array
    @return: the minimum number in the array
    """
    def findMin(self, nums):
        # write your code here
        if not nums or len(nums) == 0:
            return -1
        start = 0
        end = len(nums) - 1
        
        target = nums[len(nums) - 1]
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if nums[mid] < target:
                end = mid
            else:
                start = mid
        
        if nums[start] <= target: # trick
            return nums[start]
        else:
            return nums[end]
```
75. Find Peak Element
```python
class Solution:
    """
    @param: A: An integers array.
    @return: return any of peek positions.
    """
    def findPeak(self, A):
        # write your code here
        if not A or len(A) == 0:
            return -1
            
        start = 0
        end = len(A) - 1
        
        while(start + 1 < end):
            mid = start + (end - start) // 2
            if A[mid] > A[mid - 1]:
                start = mid
            elif A[mid] < A[mid - 1]:
                end = mid
            else:
                start = mid
        
        if A[start] < A[end]:
            return end
        else:
            return start
```
74. First Bad Version
```python
class Solution:
    """
    @param: n: An integer
    @return: An integer which is the first bad version.
    """
    def findFirstBadVersion(self, n):
        # write your code here
        if n <= 0:
            return -1
        start = 0
        end = n
        while start + 1 < end:
            mid = start + (end - start) // 2
            if SVNRepo.isBadVersion(mid):
                end = mid
            else:
                start = mid
        if SVNRepo.isBadVersion(start):
            return start
        else:
            return end
```
62. Search in Rotated Sorted Array
```python
class Solution:
    """
    @param A: an integer rotated sorted array
    @param target: an integer to be searched
    @return: an integer
    """
    def search(self, A, target):
        # write your code here
        if not A or len(A) == 0:
            return -1
        start = 0
        end = len(A) - 1
        
        while start + 1 < end:
            mid = start + (end - start) // 2
            if A[mid] == target:
                return mid
               
            elif A[mid] > A[start]:
                if A[mid] > target >= A[start]:
                    end = mid
                else:
                    start = mid
            else:
                if A[mid] < target <= A[end]:
                    start = mid
                else:
                    end = mid
                    
        if A[start] == target:
            return start
        elif A[end] == target:
            return end
        else:
            return -1
```
460. Find K Closest Elements
```python
class Solution:
    """
    @param A: an integer array
    @param target: An integer
    @param k: An integer
    @return: an integer array
    """
    def kClosestNumbers(self, A, target, k):
        # write your code here
        result = []
        if not A or len(A) == 0:
            return result
        # find the closest index
        index = self.closestIndex(A, target)
        # two pointer
        left = index - 1
        right = index
        for i in range(k):
            if left < 0:
                result.append(A[right])
                right += 1
            elif right >= len(A):
                result.append(A[left])
                left -= 1
            elif target - A[left] <= A[right] - target:
                result.append(A[left])
                left -= 1
            else:
                result.append(A[right])
                right += 1
        return result

            
    def closestIndex(self, A, target):
        
        start = 0
        end = len(A) - 1
        while start + 1 < end:
            mid = start + (end - start) // 2
            if A[mid] == target:
                return mid
            elif A[mid] < target:
                start = mid
            else:
                end = mid
        
        if target - A[start] > A[end] - target:
            return end
        else:
            return start
```
428. Pow(x, n)
```python
class Solution:
    """
    @param: x: the base number
    @param: n: the power number
    @return: the result
    """
    def myPow(self, x, n):
        # write your code here
        # Corner cases
        if n < 0:
            x = 1 / x
            n = -n
            
        ans = 1
        tmp = x
        while n != 0:
            if n % 2 == 1:
                ans *= tmp # odd n
            tmp = tmp**2 # even n
            n //= 2
        return ans
```