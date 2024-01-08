# Binary Tree - DFS

## [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

**Question**: Given the `root` of a binary tree, return its maximum depth.

**Solution**: Use Recursion + DFS to traverse the binary tree. Time complexity is `O(n)`, space complexity is `O(log(n))` (worst case is `O(n)`).

```python
def maxDepth(self, root: Optional[TreeNode]) -> int:        
    if root is None: 
        return 0 
    else: 
        left_height = self.maxDepth(root.left) 
        right_height = self.maxDepth(root.right) 
        return max(left_height, right_height) + 1 
```
