# Leet-code
In this repository, I am going to share everything I learn from LeetCode

# Integers

## Two Sum 
Problem: Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

Solution: In general, `sum` problems can be categorized into two categories: 
1) There is any array and you add some numbers to get to (or close to) a `target`
2) You need to return indices of numbers that sum up to a (or close to) a `target` value. Note that when the problem is looking for a indices, sorting the array is probably NOT a good idea.

This is the second type of the problems where we're looking for indices, so sorting is not necessary. What you'd want to do is to go over the array, and try to find two integers that sum up to a `target` value. Most of the times, in such a problem, using dictionary (hastable) helps. You try to keep track of you've observations in a dictionary and use it once you get to the results.
**Hashtable**: Hash Table is a `data structure which stores data in an associative manner`. In a hash table, data is stored in an array format, where each data value has its own unique index value. Access of data becomes very fast if we know the index of the desired data.

In this problem, you initialize a dictionary (seen). This dictionary will keep track of numbers (as key) and indices (as value). So, you go over your array (line #1) using `enumerate that gives you both index and value of elements in array`. As an example, let's do nums = [2,3,1] and target = 3. Let's say you're at index i = 0 and value = 2, ok? you need to find value = 1 to finish the problem, meaning, target - 2 = 1. 1 here is the remaining. Since remaining + value = target, you're done once you found it, right? So when going through the array, you calculate the remaining and check to see whether remaining is in the seen dictionary (line #3). If it is, you're done! you're current number and the remaining from seen would give you the output (line #4). Otherwise, you add your current number to the dictionary (line #5) since it's going to be a remaining for (probably) a number you'll see in the future assuming that there is at least one instance of answer.
```python
class Solution:
   def twoSum(self, nums: List[int], target: int) -> List[int]:
       seen = {}
       for i, value in enumerate(nums): #1
           remaining = target - nums[i] #2
           
           if remaining in seen: #3
               return [i, seen[remaining]]  #4
           else:
               seen[value] = i  #5
```


**Note:** Number is not iterable so we can't iterate through it with `for` loop.

**Note2: Python’s `map()`**  is a built-in function that allows you to process and transform all the items in an iterable without using an explicit `for` loop, a technique commonly known as mapping. `map()` is useful when you need to apply a transformation `function` to `each item` in an iterable and transform them into a new iterable.

When you compare mapping with list comprehension, it is slightly faster when you don't need lambda for defining a function.

# Strings

## Merge Strings Alternately
Problem: You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.
Return the merged string.

Let's take a look at some features about strings.
1. When you use `list()` on a string, it will automatically split the string into letters.
2. The string `join()` method returns a string by joining all the elements of an iterable (list, string, tuple), separated by the given separator.
```python
text = ['Python', 'is', 'a', 'fun', 'programming', 'language']

# join elements of text with space
print(' '.join(text))

# Output: Python is a fun programming language
```

Also let's take a look about the list's features:
1. Add Elements: There are four methods to add elements to a List in Python.
   * `append()`: append the element to the end of the list.
   * `insert()`: inserts the element before the given index.
   * `extend()`: extends the list by appending elements from the iterable.
   * List Concatenation: We can use the + operator to concatenate multiple lists and create a new list.
2. Removing Elements:
   * You can remove the item at the specified position and get its value with `pop()`. The index starts at 0 (zero-based indexing).
   * You can use `remove()` to remove the first item in the list with the specified value.

Solution:
```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        result = []
        for i in range(min(len(word1),len(word2))):
            result.append(word1[i] + word2[i])
            
        return ''.join(result) + word1[i+1:] + word2[i+1:]
```
First of all, we used min() function to get the string with less letters.
Secondly, adding to string with + is going to add the second string to the first one.
As you can see, we used join method to concat the letters of our list together.

But here's another solution that is the best possible solution:
```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        return "".join(a + b for a, b in zip(word1, word2)) + word1[len(word2):] + word2[len(word1):]
```
As you can see there is a `zip()` function. The zip() function takes iterables (can be zero or more), aggregates them in a tuple, and returns it.
In this example, because zip() gives us an iterator object, we iterate it through with inline for loop and because of that it will return a list with attached letters like ['ae', 'bf'].
**Note:** If you give a string an integer which is out of index, nothing will return (No error).
