# Arrays

The most simple form of storing data and useful for situations in which you want to iterate over every item.

Lookup operation on arrays are fast and push and pop elements of the end of the array is time efficient, however adding things at the beginning requires a loop over every item of the array because it needs to reassign the index of every element.

|Action|Time complexity  |
|--|--|
| Lookup | O(1)  |
| Push | O(1)  |
| Insert | O(n)  |
| Delete | O(n)  |

**Python Methods**
|Method| Action |
|--|--|
| append | Add elements to the end of the array |
| clear |  |
|copy  |  |
| count |Count number of element that match ``array.count("name")``  |
| extend | Append an entire list to another list O(n) |
|index  | Find the index position of an element of the array |
|insert  |  |
| pop | Remove and return the last item of the array |
|remove  |  |
| reverse | Reverse the array (e.g. last item is the first) |
| sort | Sort the array from the smallest value to the highest value or alphabetic order |


Let's do all the operation in python

```python
strings_values = ['a', 'b', 'c', 'd']

# lookup
strings_values[2] # O(1)
# Push
strings_values.append('e') # O(1)
# pop
strings_values.pop() # O(1)
# insert
strings_values.insert(0, 'x') # O(n)
# insert at the middle
strings_value.insert(4, 'alien') # O(n)
```

### Two types of arrays

**Static array**

**Dynamic array**


### Create our own array data structure

```python
class Myarray():
	def __init__(self):
		self.length = 0 # Initialize at 0
		self.data = {} # Data of the array

	def __str__(self):
		return str(self.__dict__)

	def get(self, index): # Get the data at the index
		return self.data[index]

	def push(self, item): # Add at the end of the array
		self.length += 1
		self.data[self.length-1] = item
		return self.length

	def pop(self):
		last_item = self.data[self.length-1]
		del self.data[self.length -1]
		self.length -= 1
		return last_item

	def insert(self, index, item):
		self.length += 1
		for i in range(self.length-1, index, -1):
			self.data[i] = self.data[i-1]
		self.data[index] = item

	def delete(self,index):
		for i in range(index, self.length-1):
			self.data[i] = self.data[i+1]
		del self.data[self.length-1]
		self.length -= 1
```

### Exercise

Create a function that reverses a string:
e.g.
Hi My name is Pastor
rotsaP si eman yM iH

```python
string_val =  'Hi My name is Pastor'
def reverse_string(string):
	string_reverse_list = []
	for i in range(len(string)-1,-1,-1):
		string_reverse_list.append(string[i]) # O(n)
	return "".join(string_reverse_list)
```

There are built in methods that allow to do the same thing with fewer lines of code

```python
def reverse_string(string):
	return "".join(reversed(string)) # O(n)
```

**Question**
Given two arrays that are sorted, can you merge these two arrays into one big one that is still sorted
e.g. 
[0, 3, 4, 31] 
[4, 6, 30]
Return
[0, 3, 4, 4, 6, 30, 31]

```python
array_1 = [0, 3, 4, 31] 
array_2 = [4, 6, 30]
def merge_sort(array_1, array_2):
	merge_array = array_1.copy()
	for i in array_2:
		array_1.append(i) # O(n)
	return array_1.sort()

def merge_sort(array_1, array_2):
	array_1.extend(array_2) # O(n)
	return array_1.sort()
	

```

## Static arrays


## Dynamic arrays

The problem that dynamic arrays solves is the fixed size of the static arrays. 

Let's assume that we initialize an empty array of size three. There are two components here:

1. The size of the array is three
2. The length of the array is zero

Adding elements to the end of the array is called pushing to the array. 

We also have pointers that tell us where is the last element of the array.

Deleting elements from the end of the array is called pop elements from the array, which has a constant time complexity. We update the pointer that is at the end of the array to the new last element. 

What happened if we want to add more elements beyond--in this case we need to create a new array that is able to fix the size of the new elements by double the memory since is an expensive operation and delete the old array. 

The mathematical justification on why of this is called power series. 

|Operation|Big-O Time  |
|--|--|
| r/w i-th element | O(1) |
| Insert/Remove End | O(1) |
| Insert Middle | O(n)  |
| Remove Middle | O(n) |

Suggested problems:

### 1929. Concatenation of Array

Given an integer array `nums` of length `n`, you want to create an array `ans` of length `2n` where `ans[i] == nums[i]` and `ans[i + n] == nums[i]` for `0 <= i < n` (**0-indexed**).

*Basically, this problem is asking to repeat the array two times*
```
**Input:** nums = [1,2,1]
**Output:** [1,2,1,1,2,1]
**Explanation:** The array ans is formed as follows:
- ans = [nums[0],nums[1],nums[2],nums[0],nums[1],nums[2]]
- ans = [1,2,1,1,2,1]
```

*The first idea is to iterate two times over the same array and append those values to a new array.*

*Maybe we can initialize a pointer that updates once we reach the end of the array.*

This is the complex solution

```
pointer = 0
track = 0
len_nums = len(nums)
ans = []
while track < len_nums * 2:
	track += 1
	ans.append(nums[pointer])
	pointer += 1
	if pointer == len_nums:
		pointer = 0
return ans
```

The easier solution in python will be list concatenation in python

```
nums + nums
```
