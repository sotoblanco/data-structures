## Problem: Two Number sum

|Problem| Solution | Challenge for me| Time - memory
|--|--|--|--|
|Two number sum  |1. Nested Loops 2. Hash table 3. Sorting and using pointers | Writing without highlighting  |Time O(N) Space O(N) |
| | | | |



Solution 1: Nested Loops
O(n^2) time / O(1) Space

Solution 2: Hash table
O(N) time / O(N) Space

Solution 3: Two pointers
O(n log n) time / O(1) Space

What if we cannot sort the array with .sort?


## Subsequence


## Sorted Square array

Let's explore a data structure problem using Python.  
  
Question:  
Write a function that takes in a non-empty array of integers sorted in ascending order and returns a new array of the same length with the squares of the original integers sorted in ascending order.  
  
**The first thing that comes to mind solving this problem is just to iterate over every element and square each value and append it to a new array**  
  
*This approach creates the new array, but we should ask for clarification, are negative numbers possible? The answer to this question is yes! And this is key to how to solve the problem.*  
  
**The first approach does not consider that negative numbers are possible. In that case, the square of -4 is greater than that of 3, yet the new array won't capture this order of numbers. **  
  
Let's check an example:  
  
This is the first array:  
[-4, 1, 3, 4]  
We square the array  
[16, 1, 9, 16]  
Now the array is not sorted. In that case, we can use the sorted function to get:  
[1, 9, 16, 16]  
  
**The time complexity will be O(N log N) because the sort function and the space complexity are O(n) since we store the elements in a new array.**  
  
*Note that here we are not taking advantage of the fact that the list is sorted, which can hint that the problem can be solved in constant time.*  
  
*How can we make this better?  
The first thing is to solve the issue of the negative values and take advantage of the fact that the list is sorted.*  
  
Let's try something with pointers:  
  
1. Let's assign a pointer at the beginning of the array and the end of the array.  
  
2. Compare the absolute values between the end and the beginning  
  
3. Store the square of that number at the end of the array  
  
4. Updates the pointer of the highest number to the next or previous number  
  
Time complexity: O(n)  
  
Space complexity: O(n)

```python
pointer_left = 0
pointer_right = len(array)-1
# initialize the array
square_array = [0 for _ in array]

for idx in reversed(range(len(array))):
    if abs(array[pointer_left]) > abs(array[pointer_right]):
        square_array[idx] = array[pointer_left]**2
        pointer_left += 1
    else:
        square_array[idx] = (array[pointer_right]**2)
        pointer_right -= 1
```

## Palindrome

Check if two strings is a palindrome is a must in coding interviews, the complexity of the problem can increase gradually as the interviewer ask more follow-up questions.

Question:

Write a function that takes in a non-empty string and that returns a boolean representing whether the string is a palindrome.

**If that's all that it's given, the first thing that we might think is to reverse the string and compare with the original string.**

```python
# first approach
# reverse string
string[::-1] == string
```

*Even when this can be a good start meaning that you understand the problem and won't overcomplicate things when is not required we may want to test a different approach*

Let's use a different approach where we can see other steps, maybe try a for loop

```python
# Second approach
# for loop
new = ""
for i in reversed(range(len(string))):
	new += string[i]
new == string
# Time complexity O(n^2)
# Space complexity O(n)
```
**Why the time complexity is O(n^2)?
Because string concatenation in python iterates over every element of the "new" string before adding a new one, and we iterate over every element of "string".**

Can we do a better approach?
Of course...

We can use array instead of strings

```python
new = []
for i in reversed(range(len(string))):
	new.append(string[i])
return "".join(new) == string
```

