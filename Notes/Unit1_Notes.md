# Readings: Section 1

## Section 1.1
### 1.1.4 Defining Terms
1. Statements and Expressions
  - statements typically describe actions (i.e assignment statement)
  - expressions typically describe computations - when Python evaluates an expression, it computes the value of that expression
  - example: `shakespeare = urlopen('http://composingprograms.com/shakespeare.txt')`
    - the entire statement code above is an assignment statment assigning the function to "shakespeare"
    - `urlopen` = a function to a URL that contains the complete text of William Shakespeare's 37 plays, all in a single text document
2. Functions
  -  encapsulate logic that manipulates data
  - `urlopen` is a function
3. Objects
  -  A **set** is a type of object, one that supports set operations like computing intersections and membership. An object seamlessly bundles together data and the logic that manipulates that data, in a way that manages the complexity of both.
  - Example: `{w for w in words if len(w) == 6 and w[::-1] in words}
{'redder', 'drawer', 'reward', 'diaper', 'repaid'}`
    - is a compound expression that evaluates to the set of all Shakespearian words that are simultaneously a word spelled in reverse
4. Interpreters
  - A program that implements such a procedure, evaluating compound expressions, is called an interpreter.

### 1.1.5 Errors
- debugging = method of interpreting and diagnosing errors. Tricks:
  1. **Testing incrementally**: test everything as soon as you write in, to identify the problem early. Batch by batch of new code.
  2. **Isolate Errors**: An error in the output of a statement can typically be attributed to a particular modular component. When trying to diagnose a problem, trace the error to the smallest fragment of code you can before trying to correct it.
  3. **Check your assumptions**: Check the parts you are assuming because interpreters only carry out the code that you write, no more and no less
  4. **Consult others**: Group problem solving is key.

## Section 1.2 Elements of Programming
### 1.2.1 Expressions
- **Primitive expressions**: expression that you type consists of the numerals that represent the number in base 10  - **Compound expressions**: Expressions representing numbers may be combined with mathematical operators, which the interpreter will evaluate

### 1.2.2 Call Expressions
- **call expression**: type of compound expression which applies a function to some arguments
- example: `max(7, 9)`
  - **max** = operator -> specifies a function. When this call expression is evaluated, we say that the function **max** is called with arguments 7 and 9, and returns a value of 9
  - **7, 9** = operand
- functions (i.e. `mul(5,6)`) > infix notation (i.e. `5*6`)
  - functions may take an arbitrary number of arguments
  - straightforward method of nesting functions. structure of the nesting is entirely explicit in the parentheses
  - complexity of infix notation mathematical symbols can be clarified using function notation (`*` vs `mul()`)

### 1.2.3 Importing Library Functions
- Python defines a very large number of functions, including the operator functions mentioned in the preceding section, but does not make all of their names available by default. Instead, it organizes the functions and other quantities that it knows about into modules, which together comprise the Python Library. To use these elements, one imports them.
- Example: the **math** module provides a variety of familiar math functions
  - `from math import sqrt`
  - documentation of module: <https://docs.python.org/3/library/math.html>
- An **import statement** designates a module name (e.g., operator or math), and then lists the named attributes of that module to import (e.g., sqrt). Once a function is imported, it can be called multiple times.

### 1.2.4 Names and the Evironment
- `binding` values: `radius = 10`
- names are also bound via import function: `from math import pi`
- `=` is the assignment operator
  - Assignment is our simplest means of abstraction, for it allows us to use simple names to refer to the results of compound operations
  - possibility of binding names to values and later retrieving those values by name means that the interpreter must maintain some sort of memory that keeps track of the names, values, and bindings. This memory is called an **environment**.
  - Names can also be bound to functions. For instance, the name max is bound to the max function we have been using.Functions, unlike numbers, are tricky to render as text, so Python prints an identifying description instead, when asked to describe a function: the output of `max` is `<built-in function max>`

### 1.2.5 Evaluating Nested Expressions
- How python evaluates nested expressions:
  1. Evaluate the operator and operand subexpressions, then
  2. Apply the function that is the value of the operator subexpression to the arguments that are the values of the operand subexpressions.
- Create **expression trees** to help understand how python evaluates the expressions and in what order
- A pedantic note: when we say that "a numeral evaluates to a number," we actually mean that the Python interpreter evaluates a numeral to a number. It is the interpreter which endows meaning to the programming language. Given that the interpreter is a fixed program that always behaves consistently, we can say that numerals (and expressions) themselves evaluate to values in the context of Python programs.

### 1.2.6 The Non-Pure Print Function
- **Pure Functions** = Functions have some input (their arguments) and return some output (the result of applying them)
  - input produces an output
  - i.e. abs(-2) = 2
- **Non-Pure Functions** = In addition to returning a value, applying a non-pure function can generate side effects, which make some change to the state of the interpreter or computer. A common side effect is to generate additional output beyond the return value, using the print function.
  - **Print** as an example of a non-pure functions
    -The value that print returns is always None, a special Python value that represents nothing. The interactive Python interpreter does not automatically print the value None. In the case of print, the function itself is printing output as a side effect of being called.
```
>>> print(1, 2, 3)
1 2 3
>>> print(print(1), print(2))
1
2
None None
```
    - How to understand the nested print above:
      - The inner expressions are first evaluated.
        - `print(1)` automatically outputs 1 but evaluates a none
        - `print(2)` automatically outputs 2 but evaluates a none
        - the outer print prints the values nested within, so the *None None*
  - Be careful with print! The fact that it returns None means that it should not be the expression in an assignment statement.
```
>>> two = print(2)
2
>>> print(two)
None
```
- Reasons for Sticking with Pure functions
  1. pure functions can be composed more reliably into compound call expressions
  2. pure functions tend to be simpler to test.
  3. pure functions are essential for writing concurrent programs, in which multiple call expressions may be evaluated simultaneously.

  ## Section 1.3 Defining New Functions
  ### 1.3.0 Overview
  - how to define a function
    - Function definitions consist of a *def statement* that indicates a <name> and a comma-separated list of named <formal parameters>, then a return statement, called the function body, that specifies the <return expression> of the function, which is an expression to be evaluated whenever the function is applied:
    - The second line must be indented — most programmers use four spaces to indent. The return expression is not evaluated right away; it is stored as part of the newly defined function and evaluated only when the function is eventually applied.
  ```
  def <name>(<formal parameters>):
    return <return expression>
  ```

### 1.3.1 Environments
- Environment:
  - An environment in which an expression is evaluated consists of a sequence of frames, depicted as boxes. Each frame contains bindings, each of which associates a name with its corresponding value. There is a single global frame. Assignment and import statements add entries to the first frame of the current environment.
  - Each function is a line that starts with func, followed by the function name and formal parameters. Built-in functions such as mul do not have formal parameter names, and so ... is always used instead.
  
