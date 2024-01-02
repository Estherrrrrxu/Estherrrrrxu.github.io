# Sliding Window

## 643. Maximum Average Subarray I

**Question**: Given an integer array `nums` and an integer `k`, find the maximum average value of a continuous subarray of size `k`.

**Solution**: Notice that `sum[i] = sum[i-1] + nums[i] - nums[i - k]`. Time complexity is `O(n)`, space complexity is `O(1)`.



## 1456. Maximum Number of Vowels in a Substring of Given Length

**Question**: Given a string `s` and an integer `k`, return the maximum number of vowel letters in any substring of `s` with length `k`. 

**Solution**: String version of [643](#643-maximum-average-subarray-i). Time complexity is `O(n)`, space complexity is `O(1)`.



## 1004. Max Consecutive Ones III

**Question**: Given a binary array `nums` and an integer `k`, return the maximum number of consecutive 1s in the array if you can flip at most `k` 0s.

**Solution**: Use two pointers `left` and `right` to scan the array. If `nums[right] == 0`, decrement `k`. If `k < 0`, increment `left` until `k >= 0`. Update the result. Time complexity is `O(n)`, space complexity is `O(1)`.

```python
def longestOnes(self, nums: List[int], k: int) -> int:
    left = 0
    for right in range(len(nums)):

        k -= 1 - nums[right] # nums[right] == 0: k -= 1

        # when all 0 allowance are flipped
        if k < 0:
            k += 1 - nums[left] # nums[left] == 0: k += 1
            left += 1
    # return the length of the subarray
    return right - left + 1

```



## 1493. Longest Subarray of 1's After Deleting One Element

**Question**: Return the longest subarray of a binary array `nums` after deleting one `0`.

**Solution**: Similar to [1004](#1004-max-consecutive-ones-iii). Only one small difference: it doesn't flip the 0, so `return right - left`.Time complexity is `O(n)`, space complexity is `O(1)`.