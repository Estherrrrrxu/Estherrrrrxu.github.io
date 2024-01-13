# Two Sum

This section includes two sum variations, including two sum with different data structures, two sum with different conditions, and more than two sum.

A part of the two sum problem demonstrates the trade-off of time and space complexities. If the array is sorted, two pointers is a better choice (less space). If the array is not sorted, hash table is a better choice (less time).

## [1. Two Sum](https://leetcode.com/problems/two-sum/)

**Question:** Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`, assuming there is each one pair of such numbers.

**Solution Hash Table:** For each `num` in `nums`, construct a hashtable that uses `target - num` as the key, and the index of `num` as the value. Because looking up a hashtable is $O(1)$. The time complexity is $O(N)$, and the space complexity is $O(N)$.


```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        ht = {}
        for i, num in enumerate(nums):
            if num not in ht:
                ht[target - num] = i
            # if num in ht, its complement is already in ht
            else:
                return [ht[num],i]
```

**Solution Two Pointers:** Sort the array first, then use two pointers to find the two numbers. See the below question. The time complexity is $O(NlogN)$ - for sort, and the space complexity is $O(N)$.


## [167. Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

**Question:** Given a sorted array of integers `numbers`, return the indices of two numbers that add up to `target`.

**Solution Two Pointers:** Use two pointers to find the two numbers. The time complexity is $O(N)$, and the space complexity is $O(1)$.

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers)-1
        while left < right:
            s = numbers[left] + numbers[right]
            if s < target:
                left += 1
            elif s > target:
                right -= 1
            else:
                return [left+1,right+1]
```

## [170. Two Sum III - Data structure design](https://leetcode.com/problems/two-sum-iii-data-structure-design/)

**Question:** Design and implement a TwoSum class. It should support the following operations: `add` and `find`.

**Solution:** This question inplement [ordinary Two Sum](two_sum.md##1-two-sum) with a class. The time complexity is $O(1)$ for `add` and $O(N)$ for `find`, and the space complexity is $O(N)$.

```python
class TwoSum:
    def __init__(self):
        self.array = []

    def add(self, number: int) -> None:
        self.array.append(number)

    def find(self, value: int) -> bool:
        ht = {}
        if self.array:
            for arr in self.array:
                if value - arr not in ht:
                    ht[arr] = arr
                else:
                    return True
            return False
```

## [653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

**Question:** Given the `root` of a Binary Search Tree and a target number `k`, return `true` if there exist two elements in the BST sum up to `k`.

**Solution:** Note that inorder traversal of a BST gives the nodes in ascending order. Then it is possible to get a sorted array. Then use two pointers to find the two numbers. Alternatively, can use linked list. The time complexity is $O(N)$, and the space complexity is $O(N)$.

```python
# Demonstrate inorder traversal of a BST
class Solution:
    def findTarget(self, root: Optional[TreeNode], k: int) -> bool:
        self.sorted_arr = []
        self.inorder(root)

        l, r = 0, len(self.sorted_arr)-1
        while l < r:
            summ = self.sorted_arr[l] + self.sorted_arr[r]
            if summ == k:
                return True
            elif summ < k:
                l += 1
            else: 
                r -= 1

        return False

    
    def inorder(self, root):
        if root:
            self.inorder(root.left)
            self.sorted_arr.append(root.val)
            self.inorder(root.right)
```

## [1099. Two Sum Less Than K](https://leetcode.com/problems/two-sum-less-than-k/)

**Question:** Given an array `nums` of integers and integer `k`, return the maximum `sum` such that there exists `i < j` with `nums[i] + nums[j] = sum` and `sum < k`. If no `i, j` exist satisfying this equation, return `-1`.

**Solution two pointer/binary search:**  Same as equal case, only need to track the maximum sum. The time complexity is $O(NlogN)$ - for sort, and the space complexity is $O(N)$ (best $O(logN)$).

```python
class Solution:
    def twoSumLessThanK(self, nums: List[int], k: int) -> int:
        nums = sorted(nums)
        l, r = 0, len(nums)-1

        s = -inf
        while l < r:
            summ = nums[l] + nums[r]
            if summ >= k:
                r -= 1
            else:
                l += 1
                s = max(s, summ) # add this line to track the maximum sum
        return -1 if s == -inf else s
```
**Solution counting sort:** Note that the input number range is limited to $[0, 1000]$. Hence we count each element in `nums` and store the count in `count`. Then use the same two pointers technique to find the two numbers. The time complexity is $O(N + M)$, and the space complexity is $O(M)$, where M is the values in input array.

```python
class Solution:
    def twoSumLessThanK(self, nums: List[int], k: int) -> int:

        s = -1
        count = [0] * 1001

        for num in nums:
            count[num] += 1
            
        lo = 1
        hi = 1000
        while lo <= hi:
            if lo + hi >= k or count[hi] == 0:
                hi -= 1
            else:
                if count[lo] > (0 if lo < hi else 1):
                    s = max(s, lo + hi)
                lo += 1
        return s
```

## [15. 3Sum](https://leetcode.com/problems/3sum/)

**Question:** Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`. Notice that the solution set must not contain duplicate triplets.

**Solution two pointers:** Sort the array first, iterate `i` through the `nums`, and for the rest of the array, use two pointers to find `i` and `j`. The time complexity is $O(N^2) = O(NlogN + O(N \times N))$, and the space complexity is $O(N)$.

**Solution hash table:** Similar to above solution, but using one hash table to find sum of `j` and `k`, and find `-nums[i] = nums[j] + nums[k]`. The time complexity is $O(N^2)$, and the space complexity is $O(N)$.

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()

        for i in range(len(nums)):
            # remaining value cannot be <= 0
            if nums[i] > 0:
                break
            # skip first one and skip duplicates
            if i == 0 or nums[i-1] != nums[i]:
                self.twoSum(nums, i, res)

        return res

    def twoSum(self, nums: List[int], i: int, res: List[List[int]]):

        seen = set()
        k = i + 1 # after i

        while k < len(nums):
            complement = -nums[i] - nums[k]

            # j has been put in seen
            if complement in seen:
                res.append([nums[i], nums[k], complement])

                # skip duplicates
                while k + 1 < len(nums) and nums[k] == nums[k + 1]:
                    k += 1

            # appending seen j
            seen.add(nums[k])
            k += 1
```

## [259. 3Sum Smaller](https://leetcode.com/problems/3sum-smaller/)

**Question:** Given an array `nums` of `n` integers and `target`, find the number of index triplets `i, j, k` with `0 <= i < j < k < n` that satisfy the condition `nums[i] + nums[j] + nums[k] < target`.

**Solution two pointers:** Similar to above solution, but using two pointers to find `j` and `k`. The time complexity is $O(N^2)$, and the space complexity is $O(N)$.

```python
class Solution:
    def threeSumSmaller(self, nums: List[int], target: int) -> int:
        if len(nums) <= 2:
            return 0

        nums = sorted(nums)
        
        count, self.length = 0, len(nums)
        for i in range(self.length-2):
            count += self.twoSumSmaller(nums, i+1, target - nums[i])

        return count
    
    def twoSumSmaller(self, nums, i, target):
        temp_sum = 0
        l, r = i, self.length-1
        while l < r:

            if nums[l] + nums[r] < target:
                # all numbers between r and l
                temp_sum += (r - l)
                l += 1
            else:
                r -= 1
        return temp_sum
```
        
## [18. 4Sum](https://leetcode.com/problems/4sum/)

**Question:** Given an array `nums` and `target`, return all quadruplets with distinct indices sum up to `target`.

**Solution two pointers:** This is a naive extension of [3Sum](three_sum.md##15-3sum). Just like 3Sum has an outer loop to wrap up 2Sum, 4Sum has an outer loop to wrap up 3Sum. The time complexity is $O(N^3)$, and the space complexity is $O(N)$.

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:

        
        def kSum(nums: List[int], target: int, k: int) -> List[List[int]]:
            res = []
            
            # If we have run out of numbers to add, return res.
            if not nums:
                return res
            
            # There are k remaining values to add to the sum. The 
            # average of these values is at least target // k.
            average_value = target // k
            
            # We cannot obtain a sum of target if the smallest value
            # in nums is greater than target // k or if the largest 
            # value in nums is smaller than target // k.
            if average_value < nums[0] or nums[-1] < average_value:
                return res
            
            if k == 2:
                return twoSum(nums, target)
    
            for i in range(len(nums)):
                if i == 0 or nums[i - 1] != nums[i]:
                    for subset in kSum(nums[i + 1:], target - nums[i], k - 1):
                        res.append([nums[i]] + subset)
    
            return res

        def twoSum(nums: List[int], target: int) -> List[List[int]]:
            res = []
            s = set()
    
            for i in range(len(nums)):
                if len(res) == 0 or res[-1][1] != nums[i]:
                    if target - nums[i] in s:
                        res.append([target - nums[i], nums[i]])
                s.add(nums[i])
    
            return res

        nums.sort()
        return kSum(nums, target, 4)

```

## [454. 4Sum II](https://leetcode.com/problems/4sum-ii/)

**Question:** Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4` all of length `n`, return the number of tuples `(i, j, k, l)` such that each combination of `nums1[i] + nums2[j] + nums3[k] + nums4[l]` is equal to `0`.

**Solution hash table:** Similar to [Two Sum](two_sum.md##1-two-sum), use two hash tables to store the sum of `nums1` and `nums2`, and the sum of `nums3` and `nums4`. Then iterate through the two hash tables to find the number of tuples. The time complexity is $O(N^2)$, and the space complexity is $O(N^2)$.

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        # note that a + b = -(c + d)
        count = 0
        m = collections.defaultdict(int)
        for a in nums1:
            for b in nums2:
                m[a + b] += 1
                
        for c in nums3:
            for d in nums4:
                # find how many a+b
                count += m[-(c + d)]
                
        return count
```

