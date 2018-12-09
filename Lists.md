

# Lists

## [Python Lists](https://classroom.udacity.com/courses/ud1110/lessons/c06382b2-cb27-4aac-a2bd-eb754fd13914/concepts/9f46a018-d86f-4942-83d9-61abf2a9871e)

Data structures are containers that organize and group data types together. 
A list is one of the most common and basic data structures in Python.

- You can create a list with square brackets. 
- Lists can contain a mix and match of data types.

list_of_random_things = [1, 3.4, 'a string', True]

## 2 ways to retrieve the last element:
- Use len: last_element = python_list[len(python_list) - 1]
- Use negative indices:  last_element = python_list[-1]

Retrieve the last element by reducing the len by 1. 
>>> list_of_random_things[len(list_of_random_things) - 1] 
True

Alternatively, you can index from the end of a list by using negative values, where:
-1 is the last element, 
-2 is the second to last element
and so on.

>>> list_of_random_things[-1] 
True
>>> list_of_random_things[-2] 
a string

## Slice and Dice with Lists
Can pull more than one value from a list at a time by using slicing. 
When using slicing, it is important to remember that:
the lower index is inclusive and
the upper index is exclusive.

Therefore, this:

>>> list_of_random_things = [1, 3.4, 'a string', True]
>>> list_of_random_things[1:2]
[3.4]
will only return 3.4 in a list. 
Notice this is still different than just indexing a single element, because you get a list back with this indexing. 
The colon tells us to go from the starting value on the left of the colon up to, but not including, the element on the right.

If you know that you want to start at the beginning, of the list you can also leave out this value.
>>> list_of_random_things[:2]
[1, 3.4]

or to return all of the elements to the end of the list, we can leave off a final element.
>>> list_of_random_things[1:]
[3.4, 'a string', True]
This type of indexing works exactly the same on strings, where the returned value will be a string.

## Are you in OR not in?
You saw that we can also use in and not in to return a bool of whether an element exists within our list, or if one string is a substring of another.

>>> 'this' in 'this is a string'
True
>>> 'in' in 'this is a string'
True
>>> 'isa' in 'this is a string'
False
>>> 5 not in [1, 2, 3, 4, 6]
True
>>> 5 in [1, 2, 3, 4, 6]
False

## Mutability and Order
Mutability is about whether or not we can change an object once it has been created. If an object (like a list or string) can be changed (like a list can), then it is called mutable. However, if an object cannot be changed with creating a completely new object (like strings), then the object is considered immutable.

>>> my_lst = [1, 2, 3, 4, 5]
>>> my_lst[0] = 'one'
>>> print(my_lst)
['one', 2, 3, 4, 5]
As shown above, you are able to replace 1 with 'one' in the above list. This is because lists are mutable.

However, the following does not work:

>>> greeting = "Hello there"
>>> greeting[0] = 'M'
This is because strings are immutable. This means to change this string, you will need to create a completely new string.

There are two things to keep in mind for each of the data types you are using:

Are they mutable?
Are they ordered?
Order is about whether the position of an element in the object can be used to access the element. Both strings and lists are ordered. We can use the order to access parts of a list and string.

However, you will see some data types in the next sections that will be unordered. For each of the upcoming data structures you see, it is useful to understand how you index, are they mutable, and are they ordered. Knowing this about the data structure is really useful!

Additionally, you will see how these each have different methods, so why you would use one data structure vs. another is largely dependent on these properties, and what you can easily do with it!
 



## Java




Lists in Python correspond semantically something somewhere between a Java array and an ArrayList.  They can grow, and they can reference elements like x[i].
Literals and some basic operations can be stated much more neatly than in Java:
x = [1, 3, 5]  # a list
y = [8, 5]
z = x + y # concatenates:  [1, 3, 5, 8, 5]
w = y * 3 # repeated concatenation!  [8, 5, 8, 5, 8, 5]
y.append(-3) # mutates y to [8, 5, -3], like ArrayList add method.
if 3 in z:
    ....

The + and * operations also work with strings.

