# Array/String

## 1768. Merge Strings Alternately
**Question**: given two strings `word1` and `word2`, merge the string by adding letters alternatively from each string, starting from `word1`. Directly append the additional letters to the end if one string is shorter than the other.

**Solution**: Find minimum string length, create an additional result array/string and loop through the minimum string length. Append the rest to the result array/string. Time complexity: `O(n)`. Space complexity: `O(n+m)`.

**Solution alternative**: use `zip(word1, word2)` and `+` operator for string concatenation. Note: only one of `word1[len(word2):]` and `word2[len(word1):]` will be true and be appended in the end (the longer one). Use `itertools.ziplongest(word1, word2, fillvalue="")` can automatically do this. Time complexity: `O(n)`. Space complexity: `O(n+m)`.



## 1071. Greatest Common Divisor of Strings
**Question**: given two strings `s1` and `s2` and return the largest string `x` such that `x` divides both `s1` and `s2`. Definition: `s2` divides `s1` if `s1 = s2 + ... + s2`.

**Solution**: Observation: if `s1` and `s2` have a common divisor `x`, then `s1 + s2 == s2 + s1`. Then, we can take out the part of string using the gcd length `math.gcd(len(str1), len(str2))`. Otherwise `x` not exists, return `""`. Time complexity: `O(n)`. Space complexity: `O(n)`. Direct implementation of GCD algorithm using recursion to slice down the gcd string. If length of `s1` and `s2` are not equal, keep slicing down the longer string:

```python
def gcdOfStrings(self, str1: str, str2: str) -> str:

        if str1 + str2 != str2 + str1:
            return ""

        if len(str1) > len(str2):
            return self.gcdOfStrings(str1[len(str2):], str2)
        elif len(str1) < len(str2):
            return self.gcdOfStrings(str1, str2[len(str1):])
        else:
            return str1
```



## 1431. Kids With the Greatest Number of Candies

**Question**: given a size `n` array `candies` and an integer `extraCandies`, where `candies[i]` represents the number of candies that the `ith` kid has. Return a boolean array `ans` where `ans[i]` is true if the `ith` kid can have the greatest number of candies among all the kids by adding `extraCandies` candies.

**Solution**: find the maximum number of candies in the array, then loop through the array and check if `candies[i] + extraCandies >= max_candies`. Note that it is possible to directly append if-else statement. Time complexity: `O(n)`. Space complexity: `O(n)`.



## 605. Can Place Flowers

**Question**: given a bool array `flowerbed` that represents if the `ith` position is planted with a flower, and an integer `n` flowers. Return a boolean value indicating if `n` new flowers can be planted in the `flowerbed` without violating the no-adjacent-flowers rule.

**Solution 1**: Adding `0` to both ends can simplify the edge conditions. Brute force is straight forward: looping through the array and check if `flowerbed[i-1] == flowerbed[i] == flowerbed[i+1] == 0`. Time complexity: `O(n)`. Space complexity: `O(1)`.

**Solution 2**: use a sliding window (two pointers) of size 3 to check if the window is `[0, 0, 0]`. If so, set the middle element to `1` and decrease `n` by 1. Time complexity: `O(n)`. Space complexity: `O(1)`.

**Solution 3**: One additional variable: `prev`, there are 4 possibilities
| prev | cur |      action      | explanation      |
| ---- | --- | ---------------- | ---------------- |
| 0    | 0   | prev = 1, n -= 1 | plant a flower   |
| 0    | 1   | prev = 1         | cannot plant     |
| 1    | 0   | prev = 0         | plant a flower   |
| 1    | 1   | prev = 1, n += 1 | violate the rule |



## 345. Reverse Vowels of a String

**Question**: given a string `s`, reverse only all the vowels in the string and return it. The vowels are `'a'`, `'e'`, `'i'`, `'o'`, `'u'`, and they can appear in both cases.

**Solution**: use two pointers to loop through the string from both ends. If both are vowels, swap them. To convert strings, use `s = list(s)` and `"".join(s)`. Time complexity: `O(n)`. Space complexity: `O(n)`. To optimize space complexity to O(1), directly swap the characters in the string.



## 151. Reverse Words in a String

**Question**: given an input string `s`, reverse the order of the words. Return a string of the words in reverse order concatenated by a single space.

**Solution**: use `s.split()` to split the string into a list of words (and ignore the number of spaces in between). Then reverse the list and join the words by a single space. Time complexity: `O(n)`. Space complexity: `O(n)`.



## 238. Product of Array Except Self

**Question**: given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the rest elements. 

**Solution 1**: use two arrays `left` and `right` to store the product of all elements to the left and right of `nums[i]`. Then `answer[i] = left[i] * right[i]`. Time complexity: `O(n)`. Space complexity: `O(n)`.

**Solution 2**: use a single array `answer` to store the product of all elements to the left of `nums[i]`. Then loop through the array from the right and multiply the product of all elements to the right of `nums[i]` to `answer[i]`. Time complexity: `O(n)`. Space complexity: `O(1)`.



## 334. Increasing Triplet Subsequence

**Question**: given an integer array `nums`, return `true` if there exists a triple of indices `(i, j, k)` such that `i < j < k` and `nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

**Solution**: Linear scan. Use two variables `first` and `second` to track the smallest and second smallest elements, and find the third element that are greater than both `first` and `second`. Time complexity: `O(n)`. Space complexity: `O(1)`.
```python
def increasingTriplet(self, nums: List[int]) -> bool:
    # start from something very large
    first_num = second_num = inf

    for n in nums:
        if n <= first_num:
            first_num = n
        elif n <= second_num: # this make sure first_num < second_num
            second_num = n
        else: # n > first_num and n > second_num:
            return True   

    return False
```

## 443. String Compression

**Question**: given an array of characters `chars`, compress it by attaching repeated time (> 1) of each character after the character. Directly modify the array and return the length of the compressed array. 

**Solution**: use two pointers `i` and `c_ind`, one tracks current processing character and the other tracks the current position to replace. Time complexity: `O(n)`. Space complexity: `O(1)`.

```python
def compress(self, chars: List[str]) -> int:
    i = 0 # moving pointer
    c_ind = 0 # replace pointer
    
    while i < len(chars):
        length = 1

        # keep accumulating the length of the same char
        while (i + length < len(chars)) and (chars[i+length] == chars[i]):
            length += 1

        # put current char 
        chars[c_ind] = chars[i]
        c_ind += 1
        # put current repeated length
        if length > 1:
            str_length = str(length)
            chars[c_ind:c_ind+len(str_length)] = list(str_length)
            c_ind += len(str_length) 
        # jump to the next char
        i += length
        
    return c_ind
```