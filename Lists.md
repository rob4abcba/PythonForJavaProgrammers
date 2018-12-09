

# Lists

## Python

python_list = [1, 3.4, 'a string', True]

- Create with square brackets"[12,"Tom Brady"]" . 
- Can contain any mix of data types you have seen so far.

2 ways to retrieve the last element: 
- Use len: last_element = python_list[len(python_list) - 1]
- Use negative indices:  last_element = python_list[-1]


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

