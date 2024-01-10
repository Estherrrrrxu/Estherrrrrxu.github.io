# Binary Tree - BFS

The usage of `dqeue()`: `deque.popleft()` to pop, `deque.append()` to append.

## [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

**Question**: Given the `root` of a binary tree, return the right most value of each level from top to bottom.

**Solution**: Use `rightmost` list to track the right most value of each level. Use `current_q` and `next_q` to track the current level and next level. When `current_q` is empty, we know we have finished the current level, adn we can append the right most value of the current level to `rightmost` list. Then we can set `current_q` to `next_q` and `next_q` to empty list. The BFS will stop when `next_q` is empty. Time complexity is `O(n)` and space complexity is `O(d)`, where `d` is the diameter of the tree.

```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:

        if root is None:
            return []
        
        rightmost = []
        next_q = deque([root])

        while next_q:
            current_q = next_q
            next_q = deque()

            while current_q:
                node = current_q.popleft()
                
                # append non-null children to next_q
                if node.left:
                    next_q.append(node.left)
                if node.right:
                    next_q.append(node.right)
                    
            # current level is done, append the last node
            rightmost.append(node.val)

        return rightmost
```

**Solution alternative** To reduce the space complexity, we can use only one queue. We can append `None` to the queue to indicate the end of the current level. When we pop `None` from the queue, we know we have finished the current level. Then we can append the right most value of the current level to `rightmost` list. Time complexity is `O(n)` and space complexity is `O(d)`.

## [1161. Maximum Level Sum of a Binary Tree](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/)

**Question**: Given the `root` of a binary tree, return the smallest level with maximum level sum of the binary tree.

**Solution**: Use `level_sum` list to track the sum of each level. Use `current_q` and `next_q` to track the current level and next level. When `current_q` is empty, we know we have finished the current level, adn we can append the sum of the current level to `level_sum` list. Then we can set `current_q` to `next_q` and `next_q` to empty list. The BFS will stop when `next_q` is empty. Time complexity is `O(n)` and space complexity is `O(d)`, where `d` is the diameter of the tree.

```python
class Solution:
    def maxLevelSum(self, root: Optional[TreeNode]) -> int:
        
        max_sum = -inf
        min_level = level = 0

        q = deque([root])
        
        while q:
            level += 1
            level_sum = 0

            # this will fix the num of elements in one level    
            for _ in range(len(q)):
                node = q.popleft()
        
                # append children
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
                
                # sum through the level
                level_sum += node.val

            # compare the sum at the end of each level
            if level_sum > max_sum:
                max_sum = level_sum
                min_level = level

        return min_level
```
