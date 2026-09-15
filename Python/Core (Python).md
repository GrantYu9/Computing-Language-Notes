# Set Up
- !!!
# Hello World
- ```python
  print("Hello world")
  ```
# Run
- `python3 <file>`
# Python Terminal
- You can write Python from terminal if you use Python terminal
- Type and enter `python3` to enter it
# Documentation
- You can run `help(<pretty_much_anything>)` while in [[#Python Terminal]] to run the "man page"
# Update
- !!!
# Commenting
- Single line
	- `# <comment>`
- Multi line
	- ```python
	  '''
	  <comment>
	  '''
	  ```
# Naming Conventions
- !!!
# Command Line
## Installing Modules
- !!!
## Virtual Environment
### Instantiate
- `python3 -m venv .venv`
### Activate
- `source .venv/bin/activate`
### Deactivate
- `deactivate`
# Primitive Data Types
- They're actually all objects
- And they're all useless ...
## Text Type
- `str`
- Append
	- ```python
	  text = "Hello"
	  text += " World"
	  # "text" is now "Hello World"
	  ```
- `<string>.strip()`
	- Removes whitespace around a string
- `<string>.isdigit()`
	- True if only numbers
- `<string>[<start>:<stop>:<step>]`
	- Slicing a string
	- Negative indices are allowed
- `<string>.replace(<old_text>, <new_text>)`
- `<string>.upper()`
	- Changes to all upper case
- `<string>.lower()`
	- Changes to all lower case
- `<string>.find(<word>)`
	- Tries to find a word in the string
	- `-1` on fail
- `len(<string>)`
	- Length of the string
## Numeric Types
- You can underscores to improve readability of large numbers
	- E.g. `1_000`
- `int`
	- Completely dynamic
	- Usually start at $28$ bytes, overhead included
- `float`
	- Fixed size
	- $24$ bytes
	- $8$ actual bytes, $16$ bytes of overhead
- `complex`
	- Two floats, one for real, one for complex part
	- [[Complex Numbers|Complex numbers]]
	- $16$ actual bytes, $16$ bytes of overhead
## Sequence Types
- `list`
	- $56$ bytes to start
	- Like a dynamic array
	- `<name> = [<values>]`
- `tuple`
	- $40$ bytes to start
	- Immutable
	- `<name> = (<values>)`
- `range`
	- $48$ bytes to start
	- `<name> = (<lower_bound>, <upper_bound>)`
- We can specify the type by suffixing with `[]`:
	- `list[str]`
		- Means a list that only holds strings
	- `list[str | int]`
		- A list that can hold either strings or integers
## Mapping Type
- `dict`
- A hash map
- E.g.
	- ```python
	  user = {
		  "name": "Alice",
		  "age": 25
	  }
	  ```
## Boolean Type
- `bool`
	- $24$ or $28$ bytes
## Binary Types
- `bytes`
	- Immutable sequence of bytes
	- Ways to initialize
		- `<name>=b<string>`
			- Will convert to bytes
		- `<name>=bytes(5)`
			- Null bytes of specified length
		- `<name> = bytes([<values>])`
			- Bytes 
- `bytearray`
	- Mutable version of bytes
- `memoryview`
	- Similar to [[Core (C++) (CPP)#`<span>` Header|std::span]]
	- !!! 
## None Type
- `None`
	- $16$ bytes
# Casting
- We simply surround a data type as such:
	- ```python
	  num = 2
	  new_num = float(2)
	  ```
## Alternative Number Systems
- !!!
# Custom Types
## `type` Keyword
- We can define custom hints with `type`
- ```python
  type DictValue = list[str] | discord.Guild | int
  
  self._scraped_data: dict[DataType, DictValue] = {
	  DataType.ChannelNames: [],
	  DataType.Guild: None,
	  DataType.NumberOfMembers: 0
  }
  ```
# Type Hints
- !!!
# Input & Output
## Input
- `<variable> = input(<message>);`
## Output
- `print(<string>)` works with single or double quotes
- Automatically adds new line
### Raw Strings
- E.g. `print(r"C:\users\name")`
- Special symbols are treated as part of a string
### F Strings
- E.g.
	- ```python
	  name = input("Your name: ")
	  print(f"Hello, {name}!")
	  ```
### Triple Quotes
- E.g.
	- ```python
	  print('''
	  Hello,
	  hello,
	  hello!
	  ''')
	  ```
# Dunder Methods
## Sources
- [Geeks for Geeks - Dunder Methods](https://www.geeksforgeeks.org/python/dunder-magic-methods-python/)
- [Medium - Minh Le Duc - 10 Dunder Methods Every Python Developer Should Know](https://medium.com/@minhle_0210/10-dunder-methods-every-python-developer-should-know-fe2a8c6d8445)
## Introduction
- !!!
## `__add__` Dunder Method
- !!!
## `__aiter__` Dunder Method
- !!!
## `__anext__` Dunder Method
- !!
## `__base__` Dunder Method
- !!!
## `__bases__` Dunder Method
- !!!
## `__call__` Dunder Method
- !!!
## `__del__` Dunder Method
- !!!
## `__dict__` Dunder Method
- !!!
## `__enter__` Dunder Method
- !!!
## `__eq__` Dunder Method
- !!!
## `__exit__` Dunder Method
- !!!
## `__file__` Dunder Method
- !!!
## `__get__` Dunder Method
- !!!
## `__hash__` Dunder Method
- !!!
## `__init__` Dunder Method
- !!!
## `__iter__` Dunder Method
- !!!
## `__name__` Dunder Method
- !!!
## `__next__` Dunder Method
- !!!
## `__repr__` Dunder Method
- !!!
## `__set__` Dunder Method
- !!!
## `__set_name__` Dunder Method
- !!!
## `__str__` Dunder Method
- !!!
# Creating an Entry Point
- !!!
# Arithmetic
## Functions
- `+`
- `-`
- `*`
- `/`
	- True division
- `//`
	- Floor division
- `%`
	- Modulo
- `**`
	- Exponentiation
## Behaviour
- !!!
# Bitwise Operators
- Python can actually do bitwise operators on integers! We don't always have to convert to bytes
- And
	- `&`
- Or
	- `|`
- XOR
	- `^`
- Not
	- `~`
- Left shift
	- `<<`
- Right shift
	- `>>`
# Byte Manipulation
## To Bytes
### Int
- !!!
### String
- `<string>.encode(<type>)`
	- E.g. `'utf-8'`
### Hexadecimal
- `bytes.fromhex(<hex_string>)`
### Binary
- Two step process
- ```python
  byte_value = int(<binary_string>, 2) # Where 2 is the base of the numbers sytem
  single_byte = bytes([byte_value])
  ```
## From Bytes
### Int
- !!!
### String
- `<byte_data>.decode(<type>)`
	- E.g. `'utf-8'`
### Hexadecimal
- `<byte_data>.hex()`
### Binary
- !!!
# Control Flow
## Logical Operators
- `and`
- `or`
- `not`
- Literally as they are ...
## `is` Keyword
- Use to determine if two variables refer to the same object
## Conditionals
### Standard If Statement
- ```python
  x = 5
  
  if (x > 5):
	  print(f"{x} is bigger than 5")
  elif (x < 5):
	  print(f"{x} is less than 5")
  else:
	  print("5 is 5")
  ```
- No curly braces, all indentation
### Ternary Operator
- `<name> = <true_result> if <conditional> else <false_result>`
### Match Statements
- Operators as a switch statement
- E.g.
	- ```python
	  point = (1, 1)
	  
	  match point:
		  case (0, 0):
			  print("Origin")
		  case (0, y):
			  print(f"On the Y-axis at {y}")
		  case (x, 0):
			  print(f"On the X-axis at {x}")
		  case _: # Default case
			  print("...")
	  ```
- We can dereference the item in the statement
## Loops
### For Each
- There's only for each
	- ```python
	  fruits = ("Apple", "Banana", "Pear")
	  
	  for fruit in fruits:
		  print(fruit)
	  ```
- If you want to iterate, we use ranges
	- ```python
	  size = 3;
	  
	  for i in range(3):
		  print(i)
	  ```
	- Ranges have three arguments
		1. Start
		2. End
		3. Step value
	- If you write 2 arguments, omitting the 3rd one, it will be assumed the step value is plus 1
	- If you write 1 argument, omitting the first and third argument, it will be assumed your start value is 0 with a step value of plus 1
### While
- ```python
  i = 0
  
  while (true):
	  print(i)
	  i++
	  if (i = 10):
		  break
  ```
# Functions
## Introduction
- We use `def`
- ```python
  def greet(name):
	  return f"Hello, {name}!"
  ```
- We can initialize variables inside the parameter
	- ```python
	  def power_to_two(base, exponent = 2):
		  return base ** exponent
	  ```
- Functions are objects in Python, so we can pass around functions as object and call them again as such:
	- ```python
	  def decorator(function):
		  def wrapper():
			  print("Executing function!")
			  function()
			  print("Finished execution.)
		  
		  return wrapper
	  
	  @decorator
	  def sillyFunction():
		  print("Hello world.")
	  
	  def main():
		  print("Start")
		  sillyFunction()
		  print("End")
	  
	  if __name__ = "__main__":
		  main()
	  ```
## Keyword Arguments
- Sources
	- [W3 Schools](https://www.w3schools.com/python/gloss_python_function_keyword_arguments.asp)
- We can input arguments into a function without the knowledge of the positions of the arguments
- We specify the name of the argument and provide it a value
- ```python
  class Child:
	  def __init(self):
		  pass
  
  def sillyFunction(age: int, name: str, child: Child) -> None:
	  print(f"{name} might or might not be {age} years old.")
  
  def main() -> None:
	  cool_child = Child()
	  
	  sillyFunction(child = cool_child, age = 2, name = "Suzie")
  
  if __name__ == "__main__":
	  main()
  ```
	- This will run, even though the arguments are out of place, because we use keyword arguments
## Arbitrary Arguments
- Sources
	- [W3 Schools](https://www.w3schools.com/python/gloss_python_function_arbitrary_arguments.asp)
- If we do not know how many arguments a function will take, you may prefix a parameter with `*`
- The function will take a tuple of that arbitrary argument
- ```python
  def sillyFunction(*names: str) -> None:
	  print(f"Hi {names[0]}")
  
  def main():
	  sillyFunction("Bob", "Claire", "Diana")
	  
  if __name__ == "__main__":
	  main()
  ```
- Any argument beyond the first argument valid for the arbitrary argument will be included in tuple, intentional or not
	- ```python
	  def sillyFunction(*names: str) -> None:
		  print(f"Hi {names[0]}")
	  
	  def main():
		  sillyFunction("Bob", "Claire", "Diana", False)
		  
	  if __name__ == "__main__":
		  main()
	  ```
		- `False` is a boolean but Python will think it is part of `*names`
- You must have an arbitrary keyword argument beyond an arbitrary argument if you which to have more parameters
## Arbitrary Keyword Arguments
- Sources
	- [W3 Schools](https://www.w3schools.com/python/gloss_python_function_arbitrary_keyword_arguments.asp)
- We combine the idea of [[#Keyword Arguments|keyword arguments]] and [[#Arbitrary Arguments|arbitrary arguments]]. We prefix the parameter with `**`
- The function will receive a [[#Mapping Type|dictionary]]
- ```python
  def sillyFunction(**name: str) -> None:
	  print(f"And his name is John {name["john"]})
  
  def main() -> None:
	  sillyFunctioon(john = "Cena", bob = "Marley")
  
  if __name__ == "__main__":
	  main()
  ```
## Special Arguments
### `/` Argument
- Means arguments past it must be passed positionally
### `*` Argument
- We can enforce the use of keyword arguments with a `*`, not to be confused with the syntax for [[#Arbitrary Arguments|arbitrary arguments]]
	- ```python
	  def sillyFunction(*, age: int, name: str) -> None:
		  pass
	  
	  def main() -> None:
		  sillyFunction(2, "Test")
	  
	  if __name__ == "__main__":
		  main()
	  ```
		- This will not run
# Lambda Functions
- `lambda <arguments>: <expression>`
# Decorators
- A decorator is a function that takes another function and modifies its functionality
	- It's a wrapper!
- We can make decorators like any ol' function
- Python offers the `@` to decorate functions with decorators as syntactic sugar
- ```python
  def decorator(function):
	  def wrapper():
		  print("Executing function!")
		  function()
		  print("Finished executing!")
		  
	  return wrapper
  
  @decorator
  def sillyFunction():
	  print("Hello world")
  
  def main():
	  print("Start")
	  sillyFunction()
	  print("End)
  
  if __name__ = "__main__":
	  main()
  ```
- The reason we write another function inside the decorator is because the `@` actually does this behind the scenes:
	- ```python
	  sillyFunction = decorator(sillyFunction)
	  ```
		- If we do not return an object of the function, we would return `None` instead, we we can not try to shove into `sillyFunction` for a reassignment
- If we need to decorate a function that takes in arguments, state those arguments in the wrapper function
	- ```python
	  def assertNoChange(testMethod):
		  def wrapper(vehicle):
			  _assertNoGas(vehicle)
			  testMethod(vehicle)
			  _assertNoGas(vehicle)
		  
		  return wrapper
	  ```
		- Here, `testMethod()` takes in `vehicle` as an argument
# Generators
- Sources
	- [W3 Schools](https://www.w3schools.com/python/python_generators.asp)
	- [StackOverflow - Return Type](https://stackoverflow.com/questions/43658999/what-is-the-return-type-hint-of-a-generator-function)
	- [YouTube - NeuralNine -  What Does "yield from" Do in Python?](https://www.youtube.com/watch?v=byhiRuoSQzA)
## Introduction
- Generators are functions that can pause and resume execution
## Usage & the `yield` Keyword
- The `yield` keyword suspends execution, returns a value, and brings the program back to the generator
- Observe the following code and its output:
	- Code:
		- ```python
		  from collections.abc import Generator
		  
		  def generator(number: int) -> Generator[int, None, None]:
			  print("Initiating generator.\n")
			  
			  for i in range(number):
				  print("Initiating inner loop.")
				  
				  yield i
				  
				  print("Ending inner loop.\n")
			  
			  print("Ending generator.\n")
		  
		  def main() -> None:
			  print("Initiating main.\n")
			  
			  for i in generator(5):
				  print("Initiating outer loop.")
				  
				  print(i)
				  
				  print("Ending outer loop.")
			  
			  print("Ending main.")
		  
		  if __name__ == "__main__":
			  main()
		  ```
	- Output:
		- ```txt
		  !!!
		  ```
- You can actually input stuff into a generator:
	- ```python
	  ```
## `yield from` Keywords
- !!!
## Return Type
- You have to import `Generator` from [[Libraries (Python)#`collections` Module#`abc` Module|collections.abc]]
- ```python
  # !!!
  ```
- `Generator[YieldType, SendType, ReturnType]`
	- `SendType` and `ReturnType` default to `None`
# Classes
- ```python
  class Animal:
	  def __init__(self, name, age): # Constructor
		  self.name = name
		  self.age = age
	  
	  def eat(self):
		  print("Nom nom nom.")
  
  def main():
	  dog = Animal("Destroyer of Galaxies", 1)
	  dog.eat()
  
  if __name__ == "__main__":
	  main()
  ```
- Every function in a class requires `self` as an argument
## `getattr()` Function
- `getattr(object, attribute, default)`
	- Object: the object
	- Attribute: name of attribute you want
	- Default: Default value to return
- ```python
  class Bob: 
	  def do_thing(self, thing: str): 
		  method = getattr(self, "do_" + thing, None) 
		  if method: 
			  return method() 
		  else: print("Bob doesn't know how to do that")
	  
	  def _do_one(self): 
		  print("one") 
		  
	  def _do_two(self): 
		  print("two") 
	  
  def main():
	  bob = Bob()
	  
	  bob.do_thing("one")
	  bob.do_thing("two")
	  bob.do_thing("three")
  
  if __name__ == "__main__":
	  main()
  ```
	- Output:
		- ```txt
		  one
		  two
		  Bob doesn't know how to do that
		  ```
	- Yes, it even works on methods and with strings like that
# Enums
- [[Libraries (Python)#`Enum` Class|Here]]
## Introduction
- We extend the `Enum` class
- Enumerations need a value. They can be many things, including:
	- Numbers
	- Strings
## Example
- ```python
  class DataType(Enum):
	  SixSeven = 67
	  IDK = auto()
	  SillyString = "silly_string"
  ```
# Object Orientated Programming (OOP)
## Encapsulation
- Public by default
- We normally prefix a member or function with `_` to indicate we intend for it to be private, as in we literally just avoid typing it out, but it's not actually compiler enforced encapsulation, you can still just call the member or method
	- ```python
	  class Test:
		  def __init__(self):
			  self._number = 0
		  
		  def _getNumber(self):
			  return self._number
	  
	  def main():
		  test = Test()
		  
		  print(test._number)
		  print(test._getNumber())
	  
	  if __name__ == "__main__":
		  main()
	  ```
		- Both print statements will execute
- In Python, encapsulation is a developer choice and not something intended to be compiler enforced
### Name Mangling
- !!!
## Inheritence
- As such:
- ```python
  class Vehicle:
	  def __init__(self, acceleration, max_speed):
		  self._acceleration = acceleration
		  self._max_speed = max_speed
		  
		  self._current_speed = 0
	  
	  def acceleration(self):
		  if assessSpeed():
			  return
		  
		  self._current_speed += self._acceleration
		  
	  def __assessSpeed(self):
		  return self._current_speed + self._acceleration > self.__max_speed
	  
	  def getAcceleration(self):
		  return self._acceleration
	  
	  def getCurrentSpeed(self):
		  return self._current_speed
	  
	  def getMaxSpeed(self):
		  return self._max_speed
  
  class Car:
	  def __init__ (self, acceleration, max_speed):
		  super().__init__(self, acceleration, max_speed)
	  
  def main():
	  vroom_vroom = Car(1, 100)
	  vroom_vroom.accelerate()
  
  if __name__ == "__main__":
	  main()
  ```
	- We can use `super()` to refere to the parent class
## Abstraction
- !!!
# Modularity
- You just import, the name of the file you want ...
- Suppose a file `operators.py`:
	- ```python
	  def add(x, y):
		  return x + y
	  
	  def subtract(x, y):
		  return x - y
	  ```
- That you want to include in your `main.py`
- ```python
  import operators
  
  def main():
	  choice = input("What operator do you want? (a / s): ")
	  
	  if choice != 'a' and choice != 's':
		  print("Invalid choice.")
		  return
	  
	  x = int(input("1st number: "))
	  y = int(input("2nd number: "))
	  
	  if choice = 'a':
		  answer = operators.add(x, y)
	  else:
		  answer = operators.subtract(x, y)
  
  if __name__ = "__main__":
	  main()
  ```
## Including Files in Different Directories
- Just import the intended directory as a package and import the files you need
- E.g. `from source import operators`
## Terminology
- Files are modules
- Directories are packages
## Import Order
- Source: [PEPS - Style](https://peps.python.org/pep-0008/#imports)
- System libraries and standard libraries
- Third party libraries
- Personal modules
# Error Handling
## Try Except Blocks
- Similar to [[Core (Java)#Error Handling|try catch blocks]] in Java, Python uses try except blocks:
	- ```python
	  try:
		  answer = n / 0
	  except ZeroDivisionError:
		  print("One can not divide by zero.")
	  ```
- The full form is the try, except, else, finally block:
	- Try: runs the code
	- Except: tries to catch and handle the error
	- Else: executes if no exception occurs
	- Finally: always runs
- We may have multiple except blocks, but only one of each of the other types
- ```python
  def main():
	  divisor = input("Divisor: ")
	  
	  try:
		  answer = 10 / divisor
	  except ZeroDivisionError:
		  print("You may not divide by 0.")
	  except ValueError:
		  print("Enter a valid input.")
	  else:
		  print(f"Your answer is {answer}")
	  finally:
		  print("Program complete")
  
  if __name__ == "__main__":
	  main()
  ```
## Exceptions
### Behaviour
- Exceptions are all unchecked in Python
### Raising Exceptions
- Similar to [[Core (Java)#Error Handling|throwing]] an exception in Java
- We use the `raise` keyword
- ```python
  class InvalidAgeException(Exception):
	  def __init__(self):
		  super().__init__()
  
  class Person:
	  def __init__(self, name):
		  self.__name = name
		  
		  self.__age = None
	  
	  def set(self, age):
		  if (age < 0 or age > 120):
			  raise InvalidAgeException()
		  
		  self.__age = age
  
  def main():
	  bob = Person("Bob")
	  
	  try:
		  bob.set(int(input("Age: ")))
	  except ValueError:
		  print("Invalid input.")
	  except InvalidAgeException:
		  print("Invalid age")
	  else:
		  print("Age successfully assigned")
	  
  if __name__ = "__main__":
	  main()
  ```
### Catching Exceptions
- We can catch multiple exceptions:
	- ```python
	  class InvalidAgeException(Exception):
		  def __init__(self):
			  super().__init__()
	  
	  class Person:
		  def __init__(self, name):
			  self.__name = name
			  
			  self.__age = None
			  
		  def setAge(self, age):
			  if (age < 0 or age > 120):
				  raise InvalidAgeException()
			  
			  self.__age = age
	  
	  def main():
		  bob = Person("Bob")
		  
		  try:
			  bob.setAge(int(input("age: ")))
		  except TypeError, ValueError:
			  print("Invalid input.")
		  except InvalidAgeException:
			  print("Invalid age.")
		  else:
			  print("Age successfully assigned")
	  
	  if __name__ == "__main__":
		  main()
	  ```
- Or all exceptions, by using `Exception`:
	- ```python
	  def main():
		  try:
			  answer = int(input("Dividend: ")) / int(input("Divisor: ")) 
		  except Exception:
			  print("Invalid input.")
		  else:
			  print(f"Answer: {answer}.")
			  
	  if __name__ = "__main__":
		  main()
	  ```
- Or by not specifying anything at all:
	- ```python
	  def main():
		  try:
			  answer = int(input("Dividend: ")) / int(input("Divisor: ")) 
		  except:
			  print("Invalid input.")
		  else:
			  print(f"Answer: {answer}.")
			  
	  if __name__ = "__main__":
		  main()
	  ```
### Storing Exceptions as a Variable
- We use the `as` keyword, followed by the name of the variable:
	- ```python
	  def main():
		  try:
			  answer = int(input("Dividend: ")) / int(input("Divisor: ")) 
		  except Exception as exception:
			  print(f"Invalid input. Exception: {exception}.")
		  else:
			  print(f"Answer: {answer}.")
			  
	  if __name__ = "__main__":
		  main()
	  ```
### Creating Exceptions
- We simply extend the `Exception` class:
	- ```python
	  class CustomException(Exception):
		  def __init__(self):
			  super().__init__()
	  ```
## Exception Groups & `except*` Keyword
- Sources
	- [Geeks for Geeks - Exception Groups in Python](https://www.geeksforgeeks.org/python/exception-groups-in-python/)
- [[Libraries (Python)#`ExceptionGroup` Class|ExceptionGroup]] class
- We use `except*` with exception groups instead of `except`. Python will automatically find the right exception group
	- `except*` creates another ExceptionGroup but only of the type(s) specified
- ```python
  import asyncio
  
  from random import random
  
  class RandomNumberTooSmallException(Exception):
	  def __init__(self) -> None:
		  super().__init__("Random number too small.")
  
  class StupidException(Exception):
	  def __init__(self) -> None:
		  super().__init__("Stupid error.")
  
  async def fetchData(delay: int) -> float:
	  MARGIN = 0.25
	  
	  print("Initiating")
	  
	  await asyncio.sleep(delay)
	  
	  number = random()
	  
	  if number < MARGIN:
		  raise RandomNumberTooSmallException()
	  
	  print("Done.")
	  
	  return number
  
  async def sillyFunction(delay: int) -> None:
	  await asyncio.sleep(delay)
	  
	  raise StupidException()
  
  async def main() -> None:
	  LOWER = 1
	  UPPER = 6
	  
	  tasks = []
	  
	  try:
		  async with asyncio.TaskGroup() as task_group:
			  for delay in range(LOWER, UPPER):
				  tasks.append(task_group.create_task(fetchData(delay)))
			  
			  tasks.append(task_group.create_task(sillyFunction(UPPER + 1)))
	  except* RandomNumberTooSmallException as exceptions:
		  for exception in exceptions.exceptions:
			  print(exception)
	  except* StupidException as exceptions:
		  for exception in exceptions.exceptions:
			  print(exception)
	  else:
		  print("Omg, no errors!")
	  
	  for task in tasks:
		  if task.done() and not task.cancelled():
			  try:
				  print(task.result())
			  except Exception:
				  pass
  
  if __name__ = "__main__":
	  async.run(main())
  ```
# Resource Management
## Context Managers
- Context managers allow for the safe usage of resources, handling errors when need be
- Context managers must have the following structure:
	- ```python
	  class CustomContextManager:
		  def __enter__(self):
			  pass
		  
		  def __exit__(self, exc_type, exc_val, exc_tb):
			  pass
	  ```
		- Where each method must be implemented
		- Where `exc` is short for "exception"
- Context managers can be custom made
## `with` Keyword
- When we create programs, we often work with resources that have to be opened and cleaned up properly. If we open a file, we have to make sure we close it and handle exceptions properly when we attempt to read from or write to the file to prevent data loss
	- This is where the `with` keyword can help manage things
- We use `with` followed by a context manager, which can optionally be given a nickname, and a code block
	- We may open multiple context managers in a single `with` statement
	- The context manager may be the return value of a function. So it may look like we're writing just a function after the `with` keyword, but it actually returns a context manager
- The generalized syntax is:
	- ```python
	  with <context_manager> [as <name_of_object>]:
		  <code_block>
	  ```
		- We write an expression after the `with` keyword to indicate we wish to execute it under the safety of a context manager
# List Comprehension
- ```python
  import asyncio
  
  async def increment(shared_counter: list, lock: asyncio.Lock) -> None:
	  print("Initiating increment.")
	  
	  await asyncio.sleep(1)
	  
	  async with lock:
		  print("Lock acquired.")
		  
		  shared_counter[0] += 1
		  
		  print(f"Increment completed. Shared counter is now: {shared_counter[0]}.")
	  
  async def main() -> None:
	  shared_counter = [0]
	  lock = asyncio.Lock()
	  
	  await asyncio.gather(*[increment(shared_counter, lock) for i in range(3)])
  
  if __name__ == "__main__":
	  asyncio.run(main())
  ```
# Unpacking Operator
- `*`
- We use the unpacking operator before any iterable to unpack elements
- ```python
  import asyncio
  
  async def increment(shared_counter: list, lock: asyncio.Lock) -> None:
	  print("Initiating increment.")
	  
	  await asyncio.sleep(1)
	  
	  async with lock:
		  print("Lock acquired.")
		  
		  shared_counter[0] += 1
		  
		  print(f"Increment completed. Shared counter is now: {shared_counter[0]}.")
	  
  async def main() -> None:
	  shared_counter = [0]
	  lock = asyncio.Lock()
	  
	  await asyncio.gather(*[increment(shared_counter, lock) for i in range(3)])
  
  if __name__ == "__main__":
	  asyncio.run(main())
  ```
# Asynchronous Programming
- We use the keywords`aync` & `await`
- Commonly used with [[Libraries (Python)#`asyncio` Module|asyncio]] module
## Introduction
### Coroutine Functions
- A function that can be suspended and resumed
	- In Python, we establish them with `aync` and `await` keywords
- When we run a coroutine function, it returns a [[#Coroutine Objects|coroutine object]]
	- This may actually be useful in certain scenarios:
		- ```python
		  @pytest.mark.asyncio
		  async def test_foo():
			  # ...
			  
			  mock_guild.fetch_channels.return_value = self._coroutine_wrapper([mock_channel])
			  
			  # ...
		  
		  async def coroutine_wrapper(content):
			  return content
		  ```
			- In this scenario. [[Libraries (Python)#`discord.py` Library#`Guild` Class|fetch_channels]] is supposed to return a coroutine; which is exactly what we need to replicate here
### Coroutine Objects
- Implements [[Libraries (Python)#`Coroutine` Class|collections.abc.Coroutines]] abstract base class
- A coroutine object will not run unless we `await` it
## In a Function
- We label a function as asynchronous with `async` and use `await` to indicate when we can pause execution
- ```python
  import asyncio
  
  async def sillyFunction(name: str) -> None:
	  await asyncio.sleep(2)
	  print(name)
  
  async def main() -> None:
	  asyncio.create_task(sillyFunction("Bob"))
  
  if __name__ == "__main__":
	  asyncio.run(main())
  ```
## Using a Coroutine
- In order to use a coroutine, we have to use it in an asychronous environment
- ```python
  import asyncio
  
  async def sillyFunction(name: str) -> None:
	  await asyncio.sleep(2)
	  print(name)
  
  async def main() -> None:
	  asyncio.create_task(sillyFunction("Bob"))
  
  if __name__ == "__main__":
	  asyncio.run(main())
  ```
## Context Managers
- !!!
## `async for` Keywords
- !!!
