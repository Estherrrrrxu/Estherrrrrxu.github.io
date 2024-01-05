# Two Pointers

## [283. Move Zeros](https://leetcode.com/problems/move-zeroes/)

**Question**: Given an integer array `nums`, move all `0`'s to the end **in place** while maintaining the relative order of the non-zero elements.

**Solution**: pointer `i` scans the array, pointer `curr` tracks current position of non-zero elements. Assigning non-zero elements to `nums[curr]` and let the rest of array be 0 is not optimal, because it requires array to write `n` times. Instead, we can swap `nums[i]` and `nums[curr]` to achieve the same result. Time complexity is `O(n)`, space complexity is `O(1)`.



## [392. Is Subsequence](https://leetcode.com/problems/is-subsequence/)

**Question**: Given two strings `s` and `t`, check if `s` is a subsequence of `t`.

**Solution**: Two pointers `i` and `j` scan `s` and `t` respectively. If `s[i] == t[j]`, increment both `i` and `j`. Otherwise, increment `j` only. If `i == len(s)`, return `True`. If `j == len(t)`, return `False`. Time complexity is `O(n)`, space complexity is `O(1)`.



## [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

**Question**: Given a size `n` array `height` incidicating the height of a bar at each location, find the maximum area of water that can be contained between two bars.

**Solution**: Brute force take `O(n^2)` time. Instead, use two pointers `left` and `right` to scan the array, and move the pointer with smaller height. Time complexity is `O(n)`, space complexity is `O(1)`.



## [1679. Max Number of K-Sum Pairs](https://leetcode.com/problems/max-number-of-k-sum-pairs/)

**Question**: Given an integer array `nums` and an integer `k`, return the number of pairs that sum up to `k`. Note that the pairs cannot overlap.

**Solution 1**: Use a hash table to store the frequency of each number. Scan the array, if `k - nums[i]` is in the hash table, increment the result and decrement the frequency of `k - nums[i]`. Time complexity is `O(n)`, space complexity is `O(n)`.

**Solution 2**: Sort the array. Use two pointers `left` and `right` to scan the array. If `nums[left] + nums[right] == k`, increment the result and move both pointers. If `nums[left] + nums[right] < k`, move `left` pointer. If `nums[left] + nums[right] > k`, move `right` pointer. Time complexity is `O(nlogn)`, space complexity is `O(1)`.