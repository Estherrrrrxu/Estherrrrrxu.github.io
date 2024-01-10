# Binary Tree - DFS

For this type of question, it commonly has two types of solution: recursion and iteration. Recursion is usually more intuitive to traverse the tree. If iteration is used, then a stack is needed to store the nodes.

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

## [872. Leaf Similar Trees](https://leetcode.com/problems/leaf-similar-trees/)

**Question**: Given the roots of two binary trees `root1` and `root2`, return `true` if the leaf value sequence of `root1` and the leaf value sequence of `root2` are the same, and `false` otherwise.

**Solution**: Use Recursion + DFS to traverse the binary tree. Time complexity is `O(T1+T2)`, and space complexity is `O(T1+T2)`. `T1` and `T2` are the lengths of the given trees.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def leafSimilar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        # define a DFS search
        def dfs_search(node):
            if node:
                # if reach to the leaf
                if not node.left and not node.right:
                    # return leaf
                    yield node.val
                # search left first, then right
                yield from dfs_search(node.left)
                yield from dfs_search(node.right)

        return list(dfs_search(root1)) == list(dfs_search(root2))
```


## [1448. Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

**Question**: Given a binary tree `root`, a node `X` in the tree is named **good** if in the path from root to `X` there are no nodes with a value greater than `X`. Return the number of **good** nodes in the binary tree.

**Solution**: Use DFS + stack to iterate the tree. Time complexity is `O(n)`, space complexity is `O(n)`. Alternatively, can use DFS + recursion 

```python
def goodNodes(self, root: TreeNode) -> int:
    stack = [(root, -inf)]
    # root is always good
    num_good_nodes = 1

    while stack:
        node, max_val = stack.pop()
        # check if good node
        if node.val > max_val:
            max_val = node.val
        else:
            num_good_nodes += 1
        
        # go down
        if node.left:
            stack.append((node.left, max_val))
        
        if node.right:
            stack.append((node.right, max_val))
        
    return num_good_nodes      
```


## [437. Path Sum III](https://leetcode.com/problems/path-sum-iii/)

**Question**: Given the `root` of a binary tree and an integer `targetSum`, return the number of paths where the sum of the values along the path equals `targetSum`. The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

**Solution**: Use preorder DFS + prefix sum. Time complexity is `O(n)`, space complexity is `O(n)`.

```python
def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
    # create a hashtable to store prefix sum and residuals
    sums = defaultdict(int)
    # Note, 0 is needed when sum is achieved
    sums[0] = 1

    def dfs(node, current_sum):
        # For each node, go down starting at 0
        count = 0

        if node:
            # Sum of current prefix sum is:
            current_sum += node.val

            # Number of counts that ends at current node
            # current_sum - (current_sum - targetSum) = targetSum
            count = sums[current_sum-targetSum]

            # Increase current prefix sum
            sums[current_sum] += 1

            # Explore left and right children
            count += dfs(node.left, current_sum) + dfs(node.right, current_sum)

            # Remove value of this prefixSum (path's been explored)
            sums[current_sum] -= 1

        return count

    return dfs(root, 0)
```


## [1372. Longest ZigZag Path in a Binary Tree](https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/)

**Question**: Given a binary tree `root`, a **ZigZag path** for a binary tree alternatively takes left and right child nodes. Return the longest ZigZag path contained in that tree.

**Solution**: Use DFS + recursion. The idea is to check the left and right child of each node. If the child exists, then append the steps. Otherwise, restart the steps. Time complexity is `O(n)`, space complexity is `O(n)`.

```python
class Solution:
    def longestZigZag(self, root: Optional[TreeNode]) -> int:
        self.path_length = 0
        
        def dfs(node, go_left, steps):
            if node:
                self.path_length = max(self.path_length, steps)

                if go_left:
                    # if there is a right child, append steps
                    dfs(node.left, False, steps + 1)
                    # otherwise, restart
                    dfs(node.right, True, 1)
                else:
                    dfs(node.left, False, 1)
                    dfs(node.right, True, steps + 1)
        
        # check left childs
        dfs(root, False, 0)
        dfs(root, True, 0) # And right

        return self.path_length
```

## [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

**Question**: Given a binary tree `root`, find the lowest common ancestor (LCA) of node `p` and `q` in the tree.

**Solution**: DFS + recursion. Use a boolean flag to indicate finding `p` or `q`. LCA is the first node that has true in its both subtree recursions. Note that the LCA can be `p` or `q` itself, hence the `mid` flag is needed. Time complexity is `O(n)`, space complexity is `O(n)`.

```python
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        self.ans = None

        def dfs(node):
            if not node:
                return False
            
            # left and right recursion
            left = dfs(node.left)
            right = dfs(node.right)

            # find target value
            mid = node == p or node == q

            # 2 of left, right, mid should be true
            if left + right + mid >= 2:
                self.ans = node
            
            # return True is the node is contained within the given path
            return mid or left or right
        
        dfs(root)
        return self.ans
```


