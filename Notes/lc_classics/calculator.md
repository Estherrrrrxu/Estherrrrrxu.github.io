# Calculator questions

Calculator questions in general require the use of stack and recursion. The key is to identify the pattern of the input string and the pattern of the output.

## [224. Basic Calculator](https://leetcode.com/problems/basic-calculator/)

**Question:** Implement a calculator to evaluate string `s`, which contains only non-negative integers, `+`, `-`, `(`, `)`, and spaces.

**Solution:** `stack` to track things within `()`, `result` tracks the result of the current stage, `sign` tracks the sign of the current level, and `operand` tracks the number of the current level.

When `(` is encountered, push current `result` and the `sign` before `()` into `stack`. Then do normal operational until encounter a `)`. When `)` is encountered, pop the `sign` and the `result` before `(`, and add the current `result` to the `result` before `(`.

Time complexity: `O(N)`, Space complexity: `O(N)`.

```python
class Solution:
    def calculate(self, s: str) -> int:

        stack = []
        result = 0
        sign = 1 # 1 for positive, -1 for negative
        operand = 0 # for more than one digit

        for ch in s:
            # if it's a digit
            if ch.isdigit():
                # use operand to store more than last digit saw
                operand = (operand * 10) + int(ch)

            elif ch == '+':
                # excute hanging part
                result += sign * operand
                # reset for next set of expressions
                sign = 1
                operand = 0
            elif ch == '-':
                result += sign * operand

                sign = -1
                operand = 0
            
            elif ch == '(':
                stack.append(result)
                stack.append(sign)

                sign = 1
                result = 0
            elif ch == ')':
                # start to going backward
                result += sign * operand
                # the next is for sign
                result *= stack.pop() 
                # the end is the number
                result += stack.pop()
                # reset
                operand = 0
                
        return result + sign * operand
```

## [227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/)

**Question:** Implement a calculator to evaluate string `s`, which contains only non-negative integers, `+`, `-`, `*`, `/`, and spaces. Note if the expression contains `/`, the result should be rounded down.

**Solution:** For this question, because there is no `()`, can directly use one `stack` to track the result at the previous record and return the sum over stack. 

Time complexity: `O(N)`, Space complexity: `O(N)`.

```python
class Solution:
    def evaluate(self, operator, x, y = 0):
        if operator == "+":
            return x
        if operator == "-":
            return -x
        if operator == "*":
            return x * y
        return int(x / y)


    def calculate(self, s: str) -> int: 
        stack = []
        operand = 0
        prev_operator = '+'

        for ch in s + '+': # can be '+' or '-'
            if ch.isdigit():
                operand = operand * 10 + int(ch)
            elif ch != " ":
                if prev_operator in "*/":
                    stack.append(self.evaluate(prev_operator, stack.pop(), operand))
                else:
                    stack.append(self.evaluate(prev_operator, operand))
                operand, prev_operator = 0, ch    
    
        return sum(stack)  
```

## [772. Basic Calculator III](https://leetcode.com/problems/basic-calculator-iii/)

**Question:** Implement a calculator to evaluate string `s`, which contains only non-negative integers, `+`, `-`, `*`, `/`, `(`, `)`, and spaces. Note if the expression contains `/`, the result should be rounded down.


**Solution:** For this question, everything else are the same except for handling `(` and `)`. Time complexity: `O(N)`, Space complexity: `O(N)`.

```python
class Solution:
    def evaluate(self, operator, x, y = 0):
        if operator == "+":
            return x
        if operator == "-":
            return -x
        if operator == "*":
            return x * y
        return int(x / y)


    def calculate(self, s: str) -> int: 
        stack = []
        operand = 0
        prev_operator = '+'

        for ch in s + '+': # can be '+' or '-'
            if ch.isdigit():
                operand = operand * 10 + int(ch)

            # add a part to record sign before '('  
            elif ch == "(":
                stack.append(prev_operator)
                prev_operator = "+"

            elif ch != " ":
                if prev_operator in "*/":
                    stack.append(self.evaluate(prev_operator, stack.pop(), operand))
                else:
                    stack.append(self.evaluate(prev_operator, operand))
                
                operand, prev_operator = 0, ch    

                # when reach the end of inner expression
                if ch == ")":
                    # keep adding processed integers within parenthese
                    while type(stack[-1]) == int:
                        operand += stack.pop()
                    # pop the sign before the '()'
                    prev_operator = stack.pop()

        return sum(stack)
```

## [770. Basic Calculator IV](https://leetcode.com/problems/basic-calculator-iv/)

**Question:** Implement a calculator to evaluate string `s`, which contains only non-negative integers, `+`, `-`, `*`, `/`, `(`, `)`, and spaces. However, given a list of `evalvars` and a list of `evalints`, which are the values of the variables, evaluate the expression and return the result. Note if the expression contains `/`, the result should be rounded down.

**Solution:** For this question, I don't want to solve it. It's too complicated. I will just leave it here for future reference.

