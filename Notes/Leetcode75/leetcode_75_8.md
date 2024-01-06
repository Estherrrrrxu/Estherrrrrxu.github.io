# Linked List

## [2095. Delete the Middle Node of a Linked List](https://www.leetcode.com/problems/delete-the-middle-node-of-a-linked-list/)

**Question**: Given the `head` of a linked list, delete the middle node of the linked list and return `head` of the modified linked list. If there are two middle nodes, delete the second middle node.

**Solution**: Use two pointers, `slow` and `fast`. `slow` moves one node at a time, `fast` moves two nodes at a time. When `fast` reaches the end of the linked list, `slow` is at the middle node. Time complexity is `O(n)`, space complexity is `O(1)`.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteMiddle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head.next == None:
            return None
        # Note: initialize the two pointers at different location
        slow, fast = head, head.next.next
    
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        # Make the next node skip the original next node
        slow.next = slow.next.next
    
        return head
```

## [328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

**Question**: Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

**Solution 1**: Use two linked lists, `odds` and `evens`. `head_odds` and `head_evens` points to the beginning of both linked lists. Also use a status `isOdd` to track index odd/even state. Time complexity is `O(n)`, space complexity is `O(n)`.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # intialize two linked lists
        odds = ListNode(0) 
        evens = ListNode(0)
        # set a pointer at the beginning
        head_odds = odds
        head_evens = evens
        # loop through head
        isOdd = True
        while head: 
            if isOdd:
                odds.next = head # add head into the node
                odds = odds.next # pointer += 1
            else:
                evens.next = head
                evens = evens.next
            # reverse status
            isOdd = not isOdd
            # move to the next element
            head = head.next
        # create an end for evens     
        evens.next = None
        # skip through initial node 0
        odds.next = head_evens.next
        return head_odds.next # also skips 0
```
**Solution 2**: Directly use pointers to track the odd and even nodes. Time complexity is `O(n)`, space complexity is `O(1)`.

```python
def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    if not head:
        return head

    odd, even, head_even = head, head.next, head.next

    while even and even.next:
        odd.next = odd.next.next
        even.next = even.next.next
        odd = odd.next
        even = even.next

    odd.next = head_even
    return head
```


## [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

**Question**: Given the `head` of a singly linked list, reverse the list, and return the reversed list.

**Solution 1**: Use two pointers, `prev`, `curr`, and `next_temp` to iteratively reverse the linked list. `prev` points to the previous node, `curr` points to the current node, and `next_temp` tracks to the next node. Time complexity is `O(n)`, space complexity is `O(1)`.

```python
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    prev = None 
    curr = head

    while curr:
        # Example: now prev at None (loc 0), curr at loc 1
        # curr.next at loc 2
        next_temp = curr.next
        # loc 1 connects to loc 0
        curr.next = prev
        # move prev pointer at loc 0 to loc 1
        prev = curr
        # move curr pointer at loc 1 to loc 2
        curr = next_temp
        # Simplify: curr.next, prev, curr = prev, curr, curr.next
    # Now prev reach the end of the linked list
    return prev
```

**Solution 2**: Use recursion to reverse the linked list. Note that reverse it means swap elements with symmetric indices. Time complexity is `O(n)`, space complexity is `O(n)`.

```python
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    # condition to break the cycle
    if (not head) or (not head.next):
        return head
    
    p = self.reverseList(head.next)
    # logic: if head is current at 4
    # then head.next is 5
    # we want 5 to point to 4
    # so we do head.next.next = head
    head.next.next = head
    # set the 4.next point to None
    head.next = None
    return p
```


## [2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/)

**Question**: Given the `head` of a singly linked list, return the maximum sum of symmetric pairs in the linked list. If there are no symmetric pairs, return `0`.

**Solution**: Reverse the second half of the linked list. Then use two pointers to track the maximum sum. Time complexity is `O(n)`, space complexity is `O(1)`.

```python
def pairSum(self, head: Optional[ListNode]) -> int:
    slow, fast = head, head
    max_Sum = 0

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    # Reverse second half of the linked list.
    curr, prev = slow, None
    while curr:       
        curr.next, prev, curr = prev, curr, curr.next

    # Now prev is the head of the reversed half linked list.
    while prev:
        max_Sum = max(max_Sum, head.val + prev.val)
        head = head.next
        prev = prev.next
        
    return max_Sum
```



**Solution alternative** Using stack or list to store the values of the linked list. Time complexity is `O(n)`, space complexity is `O(n)`.

