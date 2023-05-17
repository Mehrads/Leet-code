# Leet-code
In this repository, I am going to share everything I learn from LeetCode

## Two Sum 
Problem: Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

Solution: In general, `sum` problems can be categorized into two categories: 
1) There is any array and you add some numbers to get to (or close to) a `target`
2) You need to return indices of numbers that sum up to a (or close to) a `target` value. Note that when the problem is looking for a indices, sorting the array is probably NOT a good idea.

This is the second type of the problems where we're looking for indices, so sorting is not necessary. What you'd want to do is to go over the array, and try to find two integers that sum up to a `target` value. Most of the times, in such a problem, using dictionary (hastable) helps. You try to keep track of you've observations in a dictionary and use it once you get to the results.
**Hashtable**: Hash Table is a `data structure which stores data in an associative manner`. In a hash table, data is stored in an array format, where each data value has its own unique index value. Access of data becomes very fast if we know the index of the desired data.

In this problem, you initialize a dictionary (seen). This dictionary will keep track of numbers (as key) and indices (as value). So, you go over your array (line #1) using enumerate that gives you both index and value of elements in array. As an example, let's do nums = [2,3,1] and target = 3. Let's say you're at index i = 0 and value = 2, ok? you need to find value = 1 to finish the problem, meaning, target - 2 = 1. 1 here is the remaining. Since remaining + value = target, you're done once you found it, right? So when going through the array, you calculate the remaining and check to see whether remaining is in the seen dictionary (line #3). If it is, you're done! you're current number and the remaining from seen would give you the output (line #4). Otherwise, you add your current number to the dictionary (line #5) since it's going to be a remaining for (probably) a number you'll see in the future assuming that there is at least one instance of answer.
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

