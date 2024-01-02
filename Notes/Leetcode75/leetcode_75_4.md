# Prefix Sum

## 1732. Find the Highest Altitude

**Question**: Given an array `gain` of integers, return the highest cumulative sum of numbers in the array. 

**Solution**: One variable `altitude` tracks current elevation, one variable `max_altitude` tracks maximum elevation seen. Time complexity is `O(n)`, space complexity is `O(1)`.



## 724. Find Pivot Index

**Question**: Given an array of integers `nums`, calculate the pivot index of this array. If no such index exists, return `-1`. The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.

**Solution**: Use two variables `left_sum` and `right_sum` to track the sum of left and right subarray. Time complexity is `O(n)`, space complexity is `O(1)`.

```python
def pivotIndex(self, nums: List[int]) -> int:

    # if pivot on left most index:
    left_sum = 0
    right_sum = sum(nums)

    for i in range(len(nums)):
        right_sum -= nums[i]

        if left_sum == right_sum:
            return i

        left_sum += nums[i]
        
    return -1
```