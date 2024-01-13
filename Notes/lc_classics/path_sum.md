# Path Sum

Path sum is a common problem in binary tree. It is a DFS problem. We can use recursion or stack to solve it. Note that recursion is using stack behind the scene.

The definition of binary tree node is as follows:
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

## [112. Path Sum](https://leetcode.com/problems/path-sum/)

**Question:** Given the `root` of a binary tree and an integer `targetSum`, return `true` if all the values along a **root-to-leaf** path equals `targetSum`.

**Solution stack** Create a stack to store `(node, curr_sum)` pairs. The `curr_sum` is the sum of the path from root to the current node. If the current node is a leaf node, check if `curr_sum` equals `targetSum`. If not, push the left and right child of the current node to the stack with `curr_sum` updated.


```python
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        
        stack = [(root, 0)]

        while stack: 
            node, curr_sum = stack.pop()
            curr_sum += node.val

            # right -> left, because this is a stack
            if node.right:
                stack.append((node.right, curr_sum))
            if node.left:
                stack.append((node.left, curr_sum))
            
            # is leaf node
            if not node.right and not node.left:
                # check sum of the path
                if curr_sum == targetSum:
                    return True

        return False
```

**Solution recursion** In this case, I use `targetSum -= node.val` to track the remaining sum. If the current node is a leaf node, check if `targetSum` equals `0`. If not, recursively check the left and right child of the current node.

```python
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False

        targetSum -= root.val
        if not root.left and not root.right:
            return targetSum == 0
        
        return self.hasPathSum(root.left, targetSum) \
            or self.hasPathSum(root.right, targetSum)
```
**Complexity Analysis**
- Time complexity: $O(N)$, where $N$ is the number of nodes in the tree. Each node is visited once.

- Space complexity: $O(H)$, where $H$ is the height of the tree. Worst case $O(N)$, because $H = N$ for a skewed tree. Best case $O(logN)$, because $H = logN$ for a balanced tree.

## [113. Path Sum II](https://leetcode.com/problems/path-sum-ii/)

**Question:** Given the `root` of a binary tree and an integer `targetSum`, return all **root-to-leaf** paths where each path's sum equals `targetSum`. Path should be returned as a list of node values.

**Solution recursion:** Use an outside (of recursion) list `pathList` to track all valid paths, and an inside list pathNodes to track the nodes on a subtree. Note that after traverse the subtrees, pop the nodes out. Time complexity $O(N)$, space complexity $O(H)$.

```python
class Solution:

    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        pathList = []

        self.recursion_helper(root, targetSum, [], pathList)

        return pathList
    
    def recursion_helper(self, node, resSum, pathNodes, pathList):
        
        if not node:
            return False
        
        # add current node
        pathNodes.append(node.val)
        # update remaining to be sum up
        resSum -= node.val

        if not node.left and not node.right and resSum == 0:
                pathList.append(list(pathNodes))
        else:
            self.recursion_helper(node.left, resSum, pathNodes, pathList)
            self.recursion_helper(node.right, resSum, pathNodes, pathList)
        
        # pop the node after all it's subtrees are done
        pathNodes.pop()
```

## [437. Path Sum III](https://leetcode.com/problems/path-sum-iii/)

[See This](../Leetcode75/leetcode_75_9.md##437-path-sum-iii)

## [666. Path Sum IV](https://leetcode.com/problems/path-sum-iv/)

**Question:** If the depth of a tree is smaller than `5`, then this tree can be represented by a list of three-digits integers `dpv`. `d` is the depth of the node, `p` is the position of the node in the level, and `v` is the value of the node. Given a list of `dpv` representing a binary tree, return the sum of all root-to-leaf path sum.

**Solution Stack:** Construct a tree from the list using dictionary - the key are the postion. Then use stack to traverse the tree and calculate the sum. Time complexity $O(N)$, space complexity $O(N)$.

```python
class Solution:
    def pathSum(self, nums: List[int]) -> int:
        tree = {}
        for n in nums:
            d, p, v = n//100, n//10%10, n%10
            tree[(d,p)] = v

        summ = 0
        stack = [(1,1)]

        while stack:
            # get current tree node
            d, p = stack.pop()
            v = tree[(d,p)]
            # find left and right child
            left, right = (d+1, p*2-1), (d+1, p*2)
            
            # when reach the leaves
            if left not in tree and right not in tree:
                summ += v

            # explore the tree    
            if left in tree:
                tree[left] += v
                stack.append(left)
            if right in tree:
                tree[right] += v
                stack.append(right)

        return summ
```