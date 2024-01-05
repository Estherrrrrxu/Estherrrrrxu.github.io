# Hash Map/Set

## [2215. Find the Difference of Two Arrays](https://leetcode.com/problems/find-the-difference-of-two-arrays/)

**Question**: Given two integer arrays `nums1` and `nums2`, return an array `result` such that `result[0]` is a list of elements only in `nums1` but not in `nums2`, and `result[1]` is a list of elements only in `nums2` but not in `nums1`.

**Solution**: `result = [set(nums1) - set(nums2), set(nums2) - set(nums1)]`. Time complexity is `O(n+m)`, space complexity is `O(max(n,m))`.



## [1207. Unique Number of Occurrences](https://leetcode.com/problems/unique-number-of-occurrences/)

**Question**: Given an array of integers `arr`, write a function that returns `true` if and only if the number of occurrences of each value in the array is unique.

**Solution**: `collections.Counter(arr).values()` returns a list of occurrence counts. Use `set()` to remove duplicates. If the length of the set is the same as the length of the list, then all occurrence counts are unique. Time complexity is `O(n)`, space complexity is `O(n)`.

```python
from collections import Counter
def uniqueOccurrences(self, arr: List[int]) -> bool:
    count = Counter(arr).values()
    return len(set(count)) == len(set(arr))
```



## [1657. Determine if Two Strings Are Close](https://leetcode.com/problems/determine-if-two-strings-are-close/)

**Question**: Given two strings `word1` and `word2`, return `true` if you can make both strings equal by swapping any two characters or interchange two characters. Otherwise, return `false`.

**Solution**: Observation 1. `word1` and `word2` should have same characters. Observation 2. `word1` and `word2` should have same character counts. Create a dictionary to track character counts. If the two strings have same characters and same character counts, then they are close. Time complexity is `O(n) = O(n) + O(26log(26))`, space complexity is `O(1)`.

```python
from collections import Counter

def closeStrings(self, word1: str, word2: str) -> bool:
    # 1. length of word1 and word2 should be the same
    if len(word1) != len(word2):
        return False
    # create a dictionary to track character counts
    frequency1 = Counter(word1)
    frequency2 = Counter(word2)
    # 2. word1 and word2 should have same characters
    if set(frequency1.keys()) != set(frequency2.keys()):
        return False
    # sort the dictionary by frequency
    frequency1 = dict(sorted(frequency1.items(), key=lambda item: item[1]))
    frequency2 = dict(sorted(frequency2.items(), key=lambda item: item[1]))
    # 3. word1 and word2 should have same character frequencies
    return [frequency for frequency in frequency1.values()] == [frequency for frequency in frequency2.values()]
        
```

**Solution Alternative**: Use bit manipulation to track character counts. Time complexity is `O(n)`, space complexity is `O(1)`.



## [2352. Equal Row and Column Pairs](https://leetcode.com/problems/equal-row-and-column-pairs/)

**Question**: Given a `n x n` matrix `grid`, return the number of all pairs of row and column indices `(row, col)` such that `grid[row,:] == grid[:,col]`.

**Solution**: Use a dictionary to track the frequency of each row. Then for each column, check if the column is in the dictionary. If so, add the frequency to the count. Time complexity is `O(n^2)`, space complexity is `O(n^2)`.
```python
from collections import Counter

def equalPairs(self, grid: List[List[int]]) -> int:
    count = 0
    # make the entire row as dictionary key
    row_counter = Counter(tuple(row) for row in grid)
    # find matching col
    for c in range(len(grid)):
        # assemble col name
        col = [grid[r][c] for r in range(len(grid))]
        count += row_counter[tuple(col)]
    
    return count
```

**Solution Alternative**: Use Trie. Time complexity is `O(n^2) = O(n^2) + O(n)`, space complexity is `O(n^2)`.