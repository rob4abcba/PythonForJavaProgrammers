
# Index:
- Comments
- Types
- String Concatenation
- Assignments and arithmetic
- Statement syntax
- Functions
- Function Signature variations
- if Statement
- while
- Boolean result operators
- Lists
- For Loops
- Assert
- String Formatting
- Indexing and slices
- Dictionaries/Mappings
- First Class Objects
- Classes
- Documentation
- List Comprehensions
- Doctests

# Comments
- "#" starts a Python comment to the end of the line, as 
- "//" starts one in Java.

# Types
Python data is typed
23 # int
23.0  # float (Java double)
7.3 + 23.5j # complex: note j suffix, not i for the imaginary part.
False # The boolean type is called bool, and the literals are capitalized, unlike in Java.
"Hello"  # string
'H'  # ALSO a string.  There is no separate character type.  
As long as they are paired, either quote form " or ' may be used to enclose string literals.  Python also has the special form with triple quotes that allows for multiline strings with embedded " and '.
s = "Hi"
t = 'there'
twoLines = '''I'm
here!'''

While data is typed, variable names have no fixed type.  The artificial sequence
x = 1
x="hello"
is legal.  There are no type declaratons.  All data in Python are objects.   All assignments implicitly involve pointers, but there is no notation for pointers.  Hence y=x makes y an alias for x.  With mutable objects you get into the same problems with aliases as in Java.  In Python numbers and strings are immutable, so they have no problems with aliases.

# String Concatenation
String concatenation is + as in Java, but Python does not do implict conversions to string type (str).  It must be explicit:
Java:
int x = 3
String s = "The answer is " +  x;

Python:
x = 3
s = "The answer is " + str(x)

# Assignments and arithmetic
Assignment and most arithmetic operands are like Java.  Python does not have operators  ++ or --.   Python does have the ** exponentiation operator of Basic.   The value of b ** n is bn. 

Unlike Java, there cannot be integer overflow in Python.   (This is very handy when using big numbers for cryptography.)  If an operation creates a number that is too big for normal storage in a machine word, a multword format is implicily created. In versions 2.X of Python the display of integer literals indicates their underlying storage format:  An L for Long appended to an integer stored in multiple words.  (In version 3.X, the L is omitted, as an unnecessary exposure of the implementation.)

In Python 2.X the / operator is even trickier than in Java, since you cannot tell necessarily by static analysis whether both operands are int's causing integer arithmetic to be done.  You can also use  // which always means the result is integral.  (In Python 3.X the / operator is reinterpreted to always mean floaing point arithmenic, so there is never any ambiguity.)
The result of 7 // 3 is 2.  The result of 7.3 // 3.1 is 2.0.

Python has a tuple type, and assignment in tuples is element by element, so using tuples, you can do multiple assignements and have functions return multiple results.
Compare:
Java code to swap values of x and y values:
temp = x
x= y
y = temp

Python swap:  Parentheses around the group of comma separated elements is optional.  The entire right-hand side is evaluated before the assignment is made, as with any assignment. 
  y, x = x, y

# Statement syntax
Line break delimit statements in Python.  Semicolons are only used if you want multiple statements on one line.  

A statement automatically continues over multiple lines until delimiters are matched: (...), [...], or {....}.  Often a naturally long statement without such separated delimiters can have an extra set of parentheses added, allowing the statement to be split up readably on several lines.  If including matching delimiters does not make sense, you can end a line with \
and then the next line is a continuation line.  This is best avoided, if possible, since it is hard to read, and an invisible blank after the \ means the \ is not at the end of the line, causing a nasty syntax error.  (Program editors that automatically strip trailing blanks, like idle, avoid this error.)

While blocks in Java are enclosed in braces {...}, blocks in Python always come after a heading ending in a colon, and are then consistently indented underneath.  

For instance function definitions have a heading and body:

# Functions
Java:
/** javadoc comments.... */
public static int square(int x) {
    return x*x;
}

Python:
def square(x):
    """ Python function documentation 
    - string indented just inside heading
    """
    return x*x

Note, since Python is not staticly typed, ther is no declared return type (though documentation comments are helpful!).  Python functions always do actually return something.  Python has a special object None, used much like null in Java.  If no data is specified in a return statement, or there is no return statement (like in a Java void function), Python returns None.

Instance methods are discussed and illustrated in the sample code files for defining classes, listed under Classes.

# Function Signature variations
Like Java, Python allows a sequential substitution of actual parameters for formal parameters.  Python does NOT have overloading of method names, but it has a very rich variety of other options for function signatures.  The main feature we will use is keyword parameterswith default values.  You will see these in library functions, so it is good to understand the usage even if you do not write such functions.  Consider the heading of a function definition with keyword parameters:
def f(x, y, z=0, goSlow=False):
    ...
The uninitialized parameters are at the far left.  Calls to this function must have a parameter list starting with values for all the  uninitialized parameters.
f(1, 2) # x:1, y:2, z:0, goSlow:False
and may extend, without names, part or all the way sequentially into the keyword parameters
f(1,2, 3) # x:1, y:2, z:3, goSlow:False
Further actual parameters may be added, with keyword=value, in any order and with any subset of the parameters that have not already been given a value:
f(1,2, goSlow=True) # x:1, y:2, z:0, goSlow:True
f(1,2, goSlow=True, z=3) # x:1, y:2, z:3, goSlow:True
CAUTION:  The default parameter values are evaluated at function definition time, not at execution time.  Do NOT use a mutable initializer that you intend to modify inside the function unless you WANT the effect to be remembered on the next function call using the default parameter (highly unlikely).

if Statement
Java
if (x > 3) {
    x -= 2;
    System.out.println(x);
}
y = x;

Python
if x > 3:
    x -= 2
    print x
y = x

There are no parentheses needed around a condition, but there must be a colon afterward before the indented block.  The indentation that is good formatting in Java is REQUIRED in Python.

The indentation rule makes an extra keyword useful:  elif is like else if in Java.  
if x > 0:
   print 'positive'
elif x < 0:
   print 'negative'
else:
   print 'zero'

The elif construct avoids the the extra levels of indentation that would be needed in Python with 
if x > 0:
   print 'positive'
else:
    if x < 0:
        print 'negative'
    else:
        print 'zero'

while
The syntax changes for while are like for if.
Java:
int x = 11;
while (x != 0) {
    System.out.println(x);
    x /= 2;
}

Python:
x = 11
while x != 0:
    print x
    x /= 2

Boolean result operators
The comparison operator for numbers are the same as Java.  For built-in types == is like the Java equals method.  Python uses is to mean "is the exact same object at the same address"
if thisAlias is thatAlias:
    ....

Java's boolean operators &&, ||, ! are replaced in Python by the words: and, or, not.  The condition
not (x is y)
is better writen with the operator combination "is not":
x is not y

Outside of a for statement, in is a boolean operator used for membership in a collection type.  
x in collection
and its negation
x not in collection
A primary type of collection is discussed next:

Lists
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

For-Loops
Suppose words is a Java or Python list containing  elements like "yes", "no", "maybe", then
Java:
for (String w: words) {
    w = w.toUppercase();
    System.out.println(w);
}

Python:
for w in words:
    w = w.upper()
    print w

Like in Java, this for-loop syntax works for anything with an iterator.  That includes lists, tuples, sets, ....  Also in Python, strings have an iterator that returns one character at a time.  

This iterator syntax is the only option in Python for statements.  Java has another for-loop format, commonly used to iterate through an arithmetic sequence.  This can be approximated using Python's range function.  The range function can have 1, 2 or 3 paramters:
range(5) returns [0, 1, 2, 3, 4] # range(n) returns [0, 1, ... n-1]
range(2, 5) returns [2, 3, 4] # range(k, n) returns [k, k+1, ... n-1]
range(2, 9, 3) returns [2, 5, 8] # range(k, n, d) returns [k, k+d, k+2d, ... stopping BEFORE n]
range(3, 0, -1) returns [3, 2, 1] # smart enough to know what BEFORE n means with d negative

Java:
for (int i = 2; i < 9; i +=3) 
    System.out.println(i);

Python:
for i in range(2, 9, 3):
    print i

A Java for-loop with any other format, like
for (int i = 1; i < 17; i *= 2)
    System.out.println(i);

would need to be converted to a while loop in Python:
i = i
while i < 17:
    print i
    i *= 2

The statements continue and break work as in Java.  Python has no switch statement or do while.

Sometimes an empty statement is needed.  In Java it is a simple semicolon.  In Python it is pass.  A do-nothing function would be:
def placeHolder():
    pass

Assert
Java:
assert x !=0 : "May not divide by 0";

Python:  The colon becomes a comma
assert x !=0, "May not divide by 0"

The string is optional for both Java and Python.  The default for enabling assert is backwards for Java and Python:  By default Python checks assert statements.  Assertions are turned off if optimization is explicitly requested.

String Formatting
In both cases fs ends up as "Format with 3 and Hello embedded."
Java:
int x = 3;
String s = "Hello";
String fs = String.format("Format with %s and %s embedded.", x, s);
 
Python:
x = 3
s = "Hello"
fs = "Format with {0} and {1} embedded.".format(x, s);

In Python 2.7 and 3.1+ you can leave out sequential numbering inside the braces.  Both Java and Python have many fancier options.

Indexing and slices
Java:
String s= "Compute";
char c = s.charAt(2); // 'm'
String sub1 = s.substring(1, 4);  // "omp"
String sub2 = s.substring(3);  // "pute"

Python:
s = "Compute"
c = s[2]   # "m"
sub1 = s[1:4] # "omp"
sub2 = s[3:] # "pute"

The notation wih the colon between square brackets is called a slice.  The same notation works with other sequences - lists and tuples:
x = [1, 3, 5, 7, 9]
y = x[1:4]  # [3, 5, 7]
Java has something like a slice called a view, but in Java the view mutates as the larger collection changes.  Python makes a shallow copy when a slice is used in an expression.

The len functon gives the length or size of any collection/sequence type, corresponding to length or size fields or methods in Java.
len([1, 5]) # 2
len('abc') # 3

Python has a convenient piece of syntactic sugar allowing negative indices to reference elements.  In a sequence s, s[-k] for positive k is translated into s[len(s) - k]. In particular, s[-1] is the last element of the sequence - very handy.

Dictionaries/Mappings
Java:
Map<String, String> map = new HashMap<String, String>();
map.put("Jose", "773-000-1234");
map.put("Mary", "312-555-9999");
System.out.println(map.get('Jose'));
for (String key : map.keySet()) {
     System.out.println(key);
     System.out.println(map.get(key));
}

Python:
map = dict() # untyped - does not require String and String
map['Jose'] = '773-000-1234' # only require immutable key
map['Mary'] = '312-555-9999'
print map['Jose']  
for key in map:
    print key
    print map[key] 

As in Java, Python allows the get method to read a dictionary.  There is a difference from the access via square brackets:  If 'Andy' were not a key in map, trying to read 
map['Andy'] 
would cause an exception, while 
map.get('Andy') 
would return None,

First Class Objects
First class objects can be assigned to variables and passed as parameters.  Java is limited.  In Python everything is a first class object:  In particular we will use this feature for functions and classes.  (If you want to look way beyond this course, you see modules, code blocks, parse trees, tracebacks, ... are all objects.)
For example, in mod.py the ZMod function defines and returns a new function. 
Classes
Class Use
Java:
List stuff = new ArrayList();  // avoiding generics used in practice
stuff.add("Hello")
if (stuff instanceof List)
     System.out.println("right type")


Python:
stuff = list()  # no new
stuff.append("Hello")  # same dot syntax. 
if isinstance(stuff, list):  # isinstance(object, class)
    print 'right type'
# if more than one type is OK in isinstance, give a tuple of types: isinstance(stuff, (list, tuple, set))

Class Definition
See comments and samples code in animalW.py. We will be writing several classes for mathematical objects that define operators.  See mod26A.py, first, and the more robust and complicated mod26.py. The generalization is mod.py.  Python allows multiple inheritance like C++ and unlike Java.

Static Methods (advanced)
Pure functions, not tied to object instances are generally just funtions outside a class in Python, whereas they must be static methods inside a class in Java.  If you want a function to be associated with a class, but not require instances in Python, you can use a decorator to turn a method into a static method.  
Java:
class Foo {
    static int count = 0;  // one value for whole class

    static int incCount() {
        count++;
        return count;
    }
}

Python:
class Foo:
    count=0 # one value for whole class
    
    @staticmethod
    def incCount(): # no self parameter
         Foo.count += 1
         return Foo.count

Python requires dot notation with the class name or an instance any time a static method like incCount or a class variable like count is used.  

Python also has a related, more advanced concept of a class method, that can be overridden by subclasses.  This has no analog in Java.

Documentation
Both the Java and Python libraries have standard documentation, available standalone or on the Internet, hyperlinked and with search....  Python has additional interactive features in its Shell.  The dir function, applied to an object or class, displays all the methods and fields associated with that object or class.  
dir(list)
That is fine if you just forget the precise name of a method.  You can get more information with the help function, applied to a specific function or method (without the parentheses, so it refers to the function object, but does not call it), like
help(list.append)
It can also be applied to a class or module or the string name of a module (though you may get a lot displayed!).
help('doctest')
help(list)
Just in Python
Some features that are not necessary, but handy.

List Comprehensions
In math we can write 
{(x, x2) for x in {0, 1, 2, 3, 4}}
meaning 
{(0, 0), (1, 1), (2, 4), (3, 9), (4, 16)}

In Python 2.7 and 3.X, you can use the same notation (except using x**2).  In Python 2.6 (and later) you can have the corresponding notation for lists, by enclosing in square brackets:   
[(x, x*x) for x in [0, 1, 2, 3, 4]] 
or
[(x, x*x) for x in range(5)] 
which generate
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16)]
This is a very handy notation, and way more efficient that the alternate approach with a for loop doing repeated appends:
result = []
for x in range(5):
     result.append((x, x*x))

I will likely expect you to read list comprehensions, as in bases.py, but you can still write with an explicit for-loop if you do not like the syntax.

Doctests
See the comments in recursiveTuples2.py for a doctest introduction.  See a serious use of them in mod26A.py.  Then mod26.py has an extra set of doctests at the end illustrating how to check expected exceptions.  This is a great feature of Python for simple tests.  To test clearly and completely, you can write your own code instead if you prefer.


