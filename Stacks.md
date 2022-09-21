
# Stacks

|Operation|Big-O Time|
|--|--|
| Push | O(1) |
| Pop | O(1) |
| Peek/top |O(1)  |

Stacks are a common case of dynamic arrays

Last element added to the stack is the first element remove from the stack

LIFO data structure (Last In First Out)

Implementation Python

```python
class Stack:
	def __init__(self):
		self.stack = []
	def push(self, n):
		self.stack.append(n)
	def pop(self):
		self.stack.pop(n)
```

682. Baseball Game

Let's explore a data structure problem using python.

Question:

You are keeping score for a baseball game with strange rules. The game consists of several rounds, where the scores of past rounds may affect future rounds' scores.

At the beginning of the game, you start with an empty record. You are given a list of strings  `ops`, where  `ops[i]`  is the  `ith`  operation you must apply to the record and is one of the following:

1.  An integer  `x`  - Record a new score of  `x`.
2.  `"+"`  - Record a new score that is the sum of the previous two scores. It is guaranteed there will always be two previous scores.
3.  `"D"`  - Record a new score that is double the previous score. It is guaranteed there will always be a previous score.
4.  `"C"`  - Invalidate the previous score, removing it from the record. It is guaranteed there will always be a previous score.

Return  _the sum of all the scores on the record_. The test cases are generated so that the answer fits in a 32-bit integer.

**The first thing that we can see is that there are several operations associated with a specific element of the list, so once we found the element we just run the operation and is guaranteed that the condition will match for the operation which simplifies things a lot**

*We need to iterate over every element and store in a new array that stores the new operations*

**For this problem, it seems like a rule-based problem that can be solved using conditional statements.** 

*Let's think about each condition in terms of operation of array: 
C: pop elements from the new list
D: Double the last element of the new list
+: Sum the last two elements of the new list
integers: append to the new list

```python
class Solution:
    def calPoints(self, ops: List[str]) -> int:
        points = []
        for i in ops:
            if i == "C":
                points.pop()
            elif i == "D":
                points.append(points[-1]*2)
            elif i == "+":
                points.append(points[-1] +  points[-2])
            else:
                points.append(int(i))
        return sum(points)
```

https://leetcode.com/problems/baseball-game/


Let's solve this common interview question called valid parentheses

Given a string  `s`  containing just the characters  `'('`,  `')'`,  `'{'`,  `'}'`,  `'['`  and  `']'`, determine if the input string is valid.

An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.
3.  Every close bracket has a corresponding open bracket of the same type.

**Example 1:**
```
Input: s = "()"
Output: true
```

**The first thing that comes to mind based on the examples is that the brackets are in order and there are no inside brackets.**

*If that's the case, the problem only needs to look at the previous element and see if it matches with the corresponding bracket.*

**However, inside brackets can occur, so let's explore this problem try to break it down:**

1. We can only start with an open bracket, if not the string is not valid
2. We can have as many open brackets as we want, but the first closing bracket needs to close the last open bracket added.

*The second observation gives us a major hint in this problem, so a question arise, what data structure can be used to handle last in first out?*

This problem can be solved using stacks, let's explain further:

1. We can add as many as open brackets we want at the start
2. We only care about the last one until we found the first closing bracket
3.  If it matches we keep going, if not we return false

*That's great we solve the critical aspect of the problem, now how can we make it match the open brackets with the closing brackets*

**One way to approach this is to use a hash map to store the corresponding elements**

Let's go to the code:

1. Build the hash map
2. Create the stack
3. If the character is a closing parenthesis, check for:
	3.1. The stack is not empty
	3.2. The last value of the stack match with the key of our character
4. If the value is an open bracket, append to the stack
5. Return true only if the stack is empty


```python
close_to_open = {")":"(", "]":"[", "}":"{"}
stack = []
for c in s:
	if c in close_to_open:
		# check if the stack is empty
		# and last value of the stack matches with the current
		if stack and stack[-1] == close_to_open[c]:
			stack.pop()
		else:
			return False
	else:
		stack.append(c)
return not stack
```

https://leetcode.com/problems/valid-parentheses/