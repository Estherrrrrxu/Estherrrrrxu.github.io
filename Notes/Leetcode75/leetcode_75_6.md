# Stack

## 2390. Removing Stars from a String

**Question** Given a string `s` contains stars `*`. Remove all stars and the character to its left from `s` and return the new string.

**Solution** Use a stack `new_str` to track non-star characters. If the current character is a star, `new_str.pop()`. Otherwise, `new_str.append()`. Time complexity is `O(n)` and space complexity is `O(n)`.



## 735. Asteroid Collision

**Question** Given an array `asteroids` of integers, the magnitude represent size and sign represents direction (positive to the right). Only asteroids with different direction can collide. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Return the state of the asteroids after all collisions.

**Solution** Consider the positive asteroids are barriers that the negative asteroids need to pass. Then, there are three posibilities:
1. If the negative asteroid is smaller than the positive asteroid, the negative will be destroyed.
2. If the negative asteroid is larger than the positive asteroid, the positive asteroid will be destroyed. And it will keep comparing with the next left positive asteroid.
3. If they are the same size, both will be destroyed.

Time complexity is `O(n)` and space complexity is `O(n)`.

```python
def asteroidCollision(self, asteroids: List[int]) -> List[int]:
    stack = [] 
    for x in asteroids:
        # when stack is not empty
        # and x < 0, stack[-1] > 0
        while stack and stack[-1] > 0 > x:
            # destory left positive asteroids
            if stack[-1] < abs(x):
                stack.pop()
            # destory both asteroids and out of loop
            elif stack[-1] == abs(x):
                stack.pop()
                break
            # destory negative asteroids itself
            else:
                break
        else:
            stack.append(x)
            
    return stack
```


## 394. Decode String

**Question** Given an encoded string `s`, return the decoded string. The encoding rule is `k[encoded_string]`, which means repeat `encoded_string` `k` times. Note that the brackets can be nested.

**Solution** The general idea is to start parse when encountering a right bracket `]`. By using one stack, time complexity is `O(maxK^countK n)` and space complexity is `O(sum(maxK^countK n))`. If using two stacks, one tracks multiplier and one tracks string, time complexity is `O(maxK n)` and space complexity is `O(m+n)`. `m` for letters and `n` for digits.

```python
def decodeString(self, s: str) -> str:
    if not s:
        return '' 

    stack = []   
        
    for ss in s:
        if ss != ']':
            stack.append(ss)
        elif ss == ']':
            temp = '' # get a string to store the operation
            while stack[-1] != '[':
                temp = stack.pop() + temp             
            stack.pop() # pops '['
            times = ''
            while stack and stack[-1].isdigit():
                times = stack.pop()+ times
            stack.append(temp*int(times))
            
    return ''.join(stack)
```

**Solution alternative** Using recursion will be more intuitive. Time complexity is `O(maxK n)` and space complexity is `O(n)`.
