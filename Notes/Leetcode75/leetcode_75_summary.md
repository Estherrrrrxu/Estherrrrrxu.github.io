# LeetCode 75 Study Notes


## [Array/String](leetcode_75_1.md)

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 1768 | [Merge Strings Alternately](leetcode_75_1.md#1768-merge-strings-alternately) |
| 2     | 1071 | [Greatest Common Divisor of Strings](leetcode_75_1.md#1071-greatest-common-divisor-of-strings) |
| 3     | 1431 | [Kids With the Greatest Number of Candies](leetcode_75_1.md#1431-kids-with-the-greatest-number-of-candies) |
| 4     | 605  | [Can Place Flowers](leetcode_75_1.md#605-can-place-flowers) |
| 5     | 345  | [Reverse Vowels of a String](leetcode_75_1.md#345-reverse-vowels-of-a-string) |
| 6     | 151  | [Reverse Words in a String](leetcode_75_1.md#151-reverse-words-in-a-string) |
| 7     | 238  | [Product of Array Except Self](leetcode_75_1.md#238-product-of-array-except-self) |
| 8     | 334  | [Increasing Triplet Subsequence](leetcode_75_1.md#334-increasing-triplet-subsequence) |
| 9     | 443  | [String Compression](leetcode_75_1.md#443-string-compression) |


## [Two Pointers](leetcode_75_2.md)

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 283  | [Move Zeros](leetcode_75_2.md#283-move-zeros) |
| 2     | 392  | [Is Subsequence](leetcode_75_2.md#392-is-subsequence) |
| 3     | 11   | [Container With Most Water](leetcode_75_2.md#11-container-with-most-water) |
| 4     | 1679 | [Max Number of K-Sum Pairs](leetcode_75_2.md#1679-max-number-of-k-sum-pairs) | Two Sum


## [Sliding Window](leetcode_75_3.md)

A subset of two pointers. Pointers tracks the start and end of a window. The window can be fixed size or expandable.

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 643  | [Maximum Average Subarray I](leetcode_75_3.md#643-maximum-average-subarray-i) | Fixed size sliding window
| 2     | 1456 | [Maximum Number of Vowels in a Substring of Given Length](leetcode_75_3.md#1456-maximum-number-of-vowels-in-a-substring-of-given-length) | String version of 643
| 3     | 1004 | [Max Consecutive Ones III](leetcode_75_3.md#1004-max-consecutive-ones-iii) | Expandable sliding window
| 4     | 1493 | [Longest Subarray of 1's After Deleting One Element](leetcode_75_3.md#1493-longest-subarray-of-1s-after-deleting-one-element) | 1004


## [Prefix Sum](leetcode_75_4.md)
Prefix sum is equivalent to cumulative sum. One tracks current value, one tracks the desired value.

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 1732 | [Find the Highest Altitude](leetcode_75_4.md#1732-find-the-highest-altitude) |
| 2     | 724  | [Find Pivot Index](leetcode_75_4.md#724-find-pivot-index) | Same as 1991



## [Hash Map/Set](leetcode_75_5.md)

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 2215 | [Find the Difference of Two Arrays](leetcode_75_5.md#2215-find-the-difference-of-two-arrays) |
| 2     | 1207 | [Unique Number of Occurrences](leetcode_75_5.md#1207-unique-number-of-occurrences) |
| 3     | 1657 | [Determine if Two Strings Are Close](leetcode_75_5.md#1657-determine-if-two-strings-are-close) |
| 4     | 2352 | [Equal Row and Column Pairs](leetcode_75_5.md#2352-equal-row-and-column-pairs) |



## [Stack](leetcode_75_6.md)

Stack is a LIFO data structure. It is useful when we need to track the last element or the last element that satisfies a condition.

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 2390 | [Removing Stars from a String](leetcode_75_6.md#2390-removing-stars-from-a-string) |
| 2     | 735  | [Asteroid Collision](leetcode_75_6.md#735-asteroid-collision) | Pair matching problem
| 3     | 394  | [Decode String](leetcode_75_6.md#394-decode-string) | Recursive problem



## [Queue](leetcode_75_7.md)

Queue is a FIFO data structure. It is useful when we need to track the first element or the first element that satisfies a condition.

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 933  | [Number of Recent Calls](leetcode_75_7.md#933-number-of-recent-calls) |
| 2     | 649  | [Dota2 Senate](leetcode_75_7.md#649-dota2-senate) | 


## [Linked List](leetcode_75_8.md)

| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 206  | [Reverse Linked List](leetcode_75_8.md#206-reverse-linked-list) |
| 2     | 2130 | [Maximum Twin Sum of a Linked List](leetcode_75_8.md#2130-maximum-twin-sum-of-a-linked-list) |
| 3     | 876  | [Middle of the Linked List](leetcode_75_8.md#876-middle-of-the-linked-list) |
| 4     | 141  | [Linked List Cycle](leetcode_75_8.md#141-linked-list-cycle) | 876


## [Binary Tree](leetcode_75_9.md)

[A short summary of binary tree traversal.](leetcode_75_9_p.md)

### DFS
| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 104  | [Maximum Depth of Binary Tree](leetcode_75_9.md#104-maximum-depth-of-binary-tree) |
| 2     | 872  | [Leaf-Similar Trees](leetcode_75_9.md#872-leaf-similar-trees) |
| 3     | 1448 | [Count Good Nodes in Binary Tree](leetcode_75_9.md#1448-count-good-nodes-in-binary-tree) |
| 4     | 1991 | [Find the Middle Index in Array](leetcode_75_9.md#1991-find-the-middle-index-in-array) | Also a prefix sum problem
| 5     | 1372 | [Longest ZigZag Path in a Binary Tree](leetcode_75_9.md#1372-longest-zigzag-path-in-a-binary-tree) |
| 6     | 236  | [Lowest Common Ancestor of a Binary Tree](leetcode_75_9.md#236-lowest-common-ancestor-of-a-binary-tree) | 


### BFS
| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 199  | [Binary Tree Right Side View](leetcode_75_9.md#199-binary-tree-right-side-view) |
| 2     | 1161 | [Maximum Level Sum of a Binary Tree](leetcode_75_9.md#1161-maximum-level-sum-of-a-binary-tree) |

### Binary Search Tree
| No.   | LC # |  Title                                              | Similar question
| ----- | ---- | -------------------------------------------------- | ---------------- |
| 1     | 700  | [Search in a Binary Search Tree](leetcode_75_9.md#700-search-in-a-binary-search-tree) |
| 2     | 450  | [Delete Node in a BST](leetcode_75_9.md#450-delete-node-in-a-bst) |