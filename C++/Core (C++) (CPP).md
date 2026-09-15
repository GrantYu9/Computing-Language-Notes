# Set Up
- !!!
# Hello World
- ```C++
  #include <iostream>
  
  int main(void) {
	  std::cout << "Hello world! \n";
	  
	  return 0;
  }
  ```
# Compile & Run
## Compile
- On Mac
	- `clang++ <cpp_file> -o <binary_file>`
	- If you want to use a specific version
		- `clang++ =stdc++<version> <cpp_file> -o <binary_file>``
## Run
- `./<binary_file>`
# Documentation
- If `cppman` is installed, you can run `cppman <standard_library_header>` for "man pages" on standard libraries
# Update
- !!!
# Commenting
- Single line
	- `// Comment`
- Multi line
	- ```c++
	  /*
	  <comments>
	  */
	  ```
# Naming Conventions
- `snake_case` for variables
- `camelCase` for functions
- `PascalCase` for classes
# Data Types
## Primitive
- `bool`
	- 1 byte
- `char`
	- 1 byte
	- Can also be used to store small numbers
		- Whether or not `char` is signed or not depends on the compiler
- `int`
	- 4 bytes
	- Range: $\sim\pm2\times10^9$
	- `int` is the prefered data type in the vast majority of cases, unless high performance is necessary
- `size_t`
	- Maximum size unsigned integer
		- Usually 8 byts on 64 bit system, 4 bytes on a 32 bit system
- `float`
	- 4 bytes
	- Range: $\sim[-1.2\times10^{-38},3.4\times10^{38}]$
	- Precision: 6-7 significant figures
	- A float seemingly has more range than a int, even though both are 4 bytes, because a float stores numbers in scientific format. However, as a float increases in size, because it has a limited amount of significant figures, it can not represent every single number in its range. As such, a float is generally more useful with numbers near $0$
	- `float` numbers must be suffixed with an `f` or an `F`
		- E.g. `float num = 0.01F`
- `double`
	- 8 bytes
	- Range: $\sim[-2.2\times10^{-308},1.8\times10^{308}]$
	- Precision: 15-16 significant figures
	- Floating point numbers are automatically treated as a `double` unless otherwise specified
- `void`
### Keywords
#### Modifiers
- `short`
	- 2 bytes
	- Range: $\sim\pm32,000$
- `signed`
	- Forces the type to allow $\pm$ values by using a bit
- `unsigned`
	- Forces the type to only allow values $\ge0$ 
- `long long`
	- 8 bytes
	- Range: $\sim\pm9\times10^{18}$
- `long`
	- 4 bytes on Windows but 8 bytes on Mac/Linux. As such, it is avoided due to cross-platform issues
#### Specifiers
- `static`
	- Ensures a variable lives until the program ends
##### Constants
- Always read only
- `const`
	- Can be known at run time or compile time
	- Used with variables that may change but you want to enforce as read only, such as in a for each loop
- `constexpr`
	- Can only be known at compile time
	- Used with global constants
## Derived
- Some more derived data structures from down below
	- Maps
		- [[#`<map>` Header]] 
	- Unordered maps
		- [[#`unordered_map` Header]]
	- Vectors
		- [[#`<vector>` Header]]
### Pointers
- The traditional pointer, the [[Core (C)]] pointer, is usually not recommended in modern C++ code, due to safer alternatives, such as smart pointers and [[#References|references]]
- Problems such as
	- Not freeing the memory properly
		- Not freeing memory
		- Calling `delete` twice on a pointer, which would corrupt the heap
	- Dangling pointers
	- Buffer overflows
	- Unitialized pointers
- The same as [[Core (C)]]
- ```c++
  int main(void){
	  int x = 1;
	  int* x_ptr = &x;
	  
	  return 0;
  }
  ```
- A pointer can point to another pointer
### References
- Sources
	- [StackOverflow](https://stackoverflow.com/questions/60659126/rvalue-references-in-c-with-an-easy-example)
	- [Geeks for Geeks](https://www.geeksforgeeks.org/cpp/lvalues-references-and-rvalues-references-in-c-with-examples/)
- In short, a stricter pointer
- It can not
	- Reference another reference
	- Be reassigned to reference something else
	- Allow for math to be performed on it, as in pointer arithmetic
	- Reference a null object
- These restrictions can actually prove quite useful in many cases as they remove the potential dangers of the traditional pointer
- ```c++
  int main(void){
	  int x = 1;
	  int& x_ref = x;
	  
	  return 0;
  }
  ```
#### L & RValue References
- !!!
### Functions
- [[#Functions]]
#### Function Types
- !!!
## User Defined
### Strings
- [[#`<string>` Header]]
- We declare a string with `std::string`, requiring the `<string>` header
- We can append to a string with `+=`
	- ```c++
	  std::string greeting = "Hello"; 
	  greeting += " World";
	  
	  std::cout << greeting << '\n';
	  // The output would be: "Hello World"
	  ```
- 
### Structs
- Fields and methods are public by default
- Generally, only primitives, raw pointers, and super simple functions are allowed
	- Plain old data, POD
- E.g.
	- ```c++
	  struct <struct_name> {
		  <stuff>;
		  <more_stuff>;
	  }; // Don't forget the semicolon at the end!
	  
	  <struct_name> <name>(<parameters_for_constructor>); // Initializing a struct
	  ```
### Classes
- [[Core (C++) (CPP)#^bf431b|Classes]]
### Enumerations
#### Enumeration Classes
- We can define an variable that an enumeration of members, the enumerators, a fixed set of values the variable can hold
- One should specify how many bytes they want their enumeration to take up, with the number of bytes needed correlating to how many enumerators they need. For example, a byte can handle $255$ enumerators, as a byte can also represent a maximum of $(255)_{10}$
	- We can also say, we need to choose the integer type we wish to use to represent the enumerations
- To initialize:
	- ```c++
	  enum class TrafficLight : uint8_t { // We only need a byte here
		  red,
		  yellow,
		  green
	  }; // Don't forget the semicolon!
	  
	  // To initialize a value with an enumerator, we use the following syntax
	  traffic_light a_light = traffic_light::red;
	  ```
- Different enumerations can use enumerators of the same names
	- ```c++
	  enum class TrafficLight {
		  red,
		  yellow
		  green
	  };
	  
	  enum class AppleColours {
		  red,
		  green
	  };
	  
	  // Both apple_colours and traffic_light use "green" as an enumeration, which
	  // is fine, and they have their own respective implications
	  ```
- To use the enumeration, we need to separately make a variable that can hold the enum, after the enum class is set up
	- ```c++
	  enum class TrafficLight {
		  red,
		  yellow,
		  green
	  };
	  
	  TrafficLight traffic_light = TrafficLight::red;
	  ```
# Casting
## Sources
- [CPP Reference - static_cast](https://en.cppreference.com/cpp/language/static_cast)
## Introduction
- All casts work as follows:
	-   `<cast_type><target_type>(<expression>)`
	- Return a value of type `<target_type>`
## `const_cast` (Colour)
- !!!
## `dynamic_cast` (Colour)
- !!!
## `static_cast` (Colour)
- Base-to-derived conversions, or downcasts, using `static_cast` make no runtime checks
## `reinterpret_cast` (Colour)
- Does not compile to CPU instructions, except
	- When converting betwen integers and pointers
	- Or between pointers on obscure architectures where pointer representation depends on its type
- Compile time intstruction to tell the compiler to treat `<expression>` as if it had the type `<target_type>`
# Implicit Conversion
- !!!
# `using` Keyword
- !!!
# `typename` Keyword
- !!!
# `explicit` Keyword
## Sources
- [CPP Reference](https://en.cppreference.com/cpp/language/explicit)
## Introduction
- !!!
# Input & Output
- [[#`<iostream>` Header]]
## Input
- ```c++
  #include <iostream>
  
  int main(void) {
	  int age;
	  
	  std::cout << "How old are you? ";
	  std::cin >> age;
	  std::cout << "You are " << age << " years old.\n";
	  
	  return 0;
  }
  ```
- `std::cin >>` starts reading user input and automatically identifies the data type
	- Which is awesome, unlike in [[Core (C)]] ...
## Output
- `std::cout << <...>;`
- Variables and strings can be passed through
- `std::cout << <message> << '\n';` for a newline
# Arithmetic
## Functions
- [[Congruences|Congruence modulo]]
	- `%`
- Increment and decrement
	- Pre-increment and pre decrement
		- `++x` and `--x`
	- Post-increment and post decrement
		- `x++` and `x--`
- Compound assignments
	- `x += a`
	- `x -= a`
	- `x *= a`
	- `x /= a`
	- `x %= a`
- Bitwise shorthands
	- Left shift
		- `x <<= n`
		- Multiplies `x` by $2^n$
	- Right shift
		- `x >>= n`
		- Divides `x` by $2^n$
## Formatting
- We can use `'` as a "," for large numbers
	- E.g. `int x = 1'000'000;`
### Scientific Numbers
- !!!
## Behaviour
- Given `int a = a / b`, If `b` is also an `int`, and `b` does not divide `a`, then the result will be truncated towards $0$. In other words, it will round down
	- It's just a [[Functions#Floor Function|floor]]
## Overflow
- !!!
# Bitwise
## Sources
- [CPP Reference](https://en.cppreference.com/cpp/named_req/BitmaskType)
## Operators
- `AND`
	- `&`
- `OR`
	- `|`
- `XOR`
	- `^`
- `NOT`
	- `~`
- Left shift
	- Moves bits left
	-  `x << n`
	- Multiplies `x` by $2^n$
- Right shift
	- Moves bits right
	-  `x >> n`
	- Divides `x` by $2^n$
## BitmaskType
- [[#Named Requirements#BitmaskType|Here]]
# Control Flow
## Logical Operators
- And
	- `&&`
- Or
	- `||`
- Not
	- `!`
## Conditionals
### Standard If Statement
- ```c++
  int main(void){
	  int age = 22;
	  
	  if (age > 120 || age <= 0) {
		  std::cout << "No way.\n";
	  } else if (age < 21) {
		  std::cout << "When you're older.\n";
	  } else {
		  std::cout << "Eligible.\n";
	  }
	  
	  return 0;
  }
  ```
- A continue can be added at the end of an `if` result if you want to check other cases. This can remove nested if statements
### Ternary Operator
- ```c++
  int main(void) {
	  int age = 22;
	  
	  std::string check = (age > 21) ? "Eligible.\n" : "When you're older.\n";
	  
	  return 0;
  }
  ```
- `<output_type> <variable_name> = <conditional> ? <if_result> : <else_result>`
### Switch Statements
- ```c++
  int main(void) {
	  int output;
	  
	  switch (output) {
		  case 67:
			  std::cout << "That's a lot of code!\n";
			  break;
		  case 1:
			  std::cout << "Syntax error.\n";
			  break;
		  case 2:
			  std::cout << "Out of bounds memory read.\n";
			  break;
		  default:
			  std::cout << "No errors.\n";
	  }
	  
	  return 0;
  }
  ```
- A break must included at the end of a case if you do not want to check any more cases
## Loops
### For
- ```c++
  int main(void) {
	  int n = 3;
	  
	  for (int i = 0; i < n; ++i) {
		  std::cout << i << '\n';
	  }
	  
	  return 0;
  }
  ```
#### For Each
##### Traditional
###### Read-Only
- ```c++
  int main(void) {
	  std::vector<std::string> fruits = {"Apple", "Banana", "Orange"};
	  
	  for (const std::string fruit : fruits) {
		  std::cout << fruit << ".\n";
	  }
	  
	  return 0;
  }
  ```
- We declare the type, give a name for a variable, any name, to represent each entry, add ` : `, and specify the data type we want to iterate over
###### Modify-Value
- This time, we pass in the values by reference
- ```c++
  int main(void) {
	  std::vector<std::string> fruits = {"Apple", "Banana", "Orange"};
	  
	  // By reference now
	  for (std::string& fruit : fruits) {
		  fruit += 's'; // We pluralize each entry
		  std::cout << fruit << ".\n";
	  }
	  
	  return 0;
  }
  ```
##### Modern
- We use `auto` so C++ identifies the value type for us
###### Read-Only
- ```c++
  int main(void) {
	  std::vector<std::string> fruits = {"Apple", "Banana", "Orange"};
	  
	  for (const auto fruit : fruits) {
		  std::cout << fruit << ".\n";
	  }
	  
	  return 0;
  }
  ```
- We do not use `constexpr` because when working with a loop, some values may not be known at compile time
###### Modify-Value
- ```c++
  int main(void) {
	  std::vector<std::string> fruits = {"Apple", "Banana", "Orange"};
	  
	  // By reference now
	  for (auto& fruit : fruits) {
		  fruit += 's'; // We pluralize each entry
		  std::cout << fruit << ".\n";
	  }
	  
	  return 0;
  }
  ```
### While
- ```c++
  int main(void) {
	  int i = 0;
	  int n = 5;
	  
	  while (true) {
		  if (i > n) {
			  break;
		  }
		  std::cout << i << ".\n";
		  ++i;
	  }
	  
	  return 0;
  }
  ```
### Do While
- ```c++
  int main(void) {
	  int i = 0;
	  int n = 5;
	  
	  do {
		  if (i > n) {
			  break;
		  }
		  std::cout << i << ".\n";
		  ++i;
	  } while (true);
	  
	  return 0;
  }
  ```
- Executes content in the code block once, then continues running while the `while` expression is true or until a break occurs
# Visibility
## Forward Declaration
- !!!
# Command Line
## Arguments
- To allow arguments, we do this:
	- ```c++
	  #include <iostream>
	  
	  int main(int argc, char* argv[]) {
		  // Stub ...
		  
		  return 0;
	  }
	  ```
- To pass in arguments, we do this:
	- `./tideman Alice Bob Charlie`
		- If the program's name were `tideman`
	- `Alice`, `Bob`, and `Charlie` are the arguments and the OS will do the dirty work of parsing them, converting them into a string array, and counting them
- Note that the last element of `argv[]` is `NULL`, so `argv[argc] == NULL`
# Memory
## Sources
- !!!
## Introduction
- !!!
## Pointers & References
- !!!
## Management
### `sizeof` Keyword
- !!!
### Allocation
- !!!
### Clean Up
- !!!
## RAII & Modern Memory Management
- !!!
# Functions
- A type of [[#Derived|derived]] data type
- A function must have an output data type, a name, and input types
- A function must be forward declared via typing a function prototype at the top if the function body is below the `main` function
- ```c++
  #include <iostream>
  
  // Function prototype 
  int sum(int x, int y);
  
  int main(void){
	  int x = 1;
	  int y = 2;
	  
	  std::cout << "The sum is: " << sum(x, y) << ".\n";
	  
	  return 0;
  }
  
  // The actual function body down below
  int sum(int x, int y) {
	  return x + y;
  }
  ```
## Overloading
### Function Overloading
- When multiple functions of identical names are allowed due to the following possibilities of differences
	- Number of arguments
	- Types of arguments
	- Order of arguments
- E.g.
	- ```c++
	  int sum(int a, int b);
	  double sum(double a, double b);
	  // "sum" is overloaded; we have different types
	  ```
### Operator Overloading
- We can make operator exhibit custom behaviour
- E.g.
	- ```c++
	  <output_type> operator<operator>(<parameters>) {
		  return <something>;
	  }
	  ```
# Lambda Functions
- `[<capture>](<parameters>){<function>;}(<operands>)`
- !!!
# Classes
^bf431b
- A type of [[#User Defined|user defined]] data type
## Sources
- [Geeks for Geeks - Inheritance - Visibility Modes](https://www.geeksforgeeks.org/cpp/visibility-modes-in-c-with-examples/)
- [Geeks for Geeks - Polymorphism - Method Overriding]
- [Geeks for Geeks - vTable & vPtr in C++](https://www.geeksforgeeks.org/cpp/vtable-and-vptr-in-cpp/)
## Introduction
- Fields and methods are private by default
- We declare a class as such
	- ```c++
	  #include <iostream>
	  
	  class Employee {
		  <code>;
	  }; // Don't forget the semicolon at the end!
	  
	  int main(void) {
		  return 0; 
	  }
	  ```
	- It is declared outside and above the main function
- We can put some values inside the class as well as methods, which are functions inside a class
	- ```c++
	  #include <iostream>
	  
	  class Employee {
		  int age;
		  
		  void stateAge() {
			  std::cout << age; 
		  }
		  void resetAge(int age) {
			  this->age = age;
		  } 
	  };
	  
	  int main(void) {
		  return 0;
	  }
	  ```
- Methods and functions can not share a name
## Constructors
- A constructor allows for a class to be initialized
- The best way to form a constructor is with a member intializer list, where the values can be initialized upon creation of an object
- Example // !!! is constexpr in private valid
	- ```c++
	  #include <iostream>
	  
	  class Employee {
	  private:
		  constexpr int ID_NUMBER;
		  
		  int age;
	  public:
		  Employee(constexpr int ID_NUMBER, int age_input) : ID_NUMBER(ID_NUMBER), age(age_input) {
			  // Stub ...
		  }
	  };
	  
	  int main(void) {
		  Employee Bob(123456789, 23); 
		  
		  return 0;
	  }
	  ```
## Access Modifiers
- Types of access modifiers
	- `private`
		- Only the class can see these
	- `protected`
		- Only the class and derived class can see this
		- What's a derived class? Head over to [[Object Orientated Design (OOD)|this]] page
	- `public`
		- Anyone using the class can see these
- Usually `private` and `public` are used
- Example
	- ```c++
	  #include <iostream>
	  
	  class Employee {
	  private:
		  int age;
	  public:
		  void stateAge() {
			  std::cout << age; 
		  }
		  void setNewAge(int age) {
			  this->age = age;
		  }
		  
		  Employee(int age)
			  : age(age) {}
	  };
	  
	  int main(void) {
		  Employee Bob(23); 
		  
		  Bob.setNewAge(24);
		  
		  return 0;
	  }
	  ```
	- This way, when we want to change Bob's age, we iteract with the class via the methods, protecting the sensitive data
## Stack versus Heap Allocation
### Stack Allocation
- We use direct or uniform initialization
- ```cpp
  #include <string>
  
  class Person {
  private:
	  std::string name; 
	  
  public:
	  Person(std::string name) : name(name) {}
  };
  
  int main(void) {
	  Person bob("Bob"); // Direct
	  
	  Person alice{"Alice"}; // Uniform
	  
	  return 0;
  }
  ```
### Heap Allocation
- We use the `new` keyword
- ```cpp
  #include <string>
  
  class Person {
  private:
	  std::string name;
  
  public:
	  Person(std::string name) : name(name) {}
  };
  
  int main(void) {
	  Person* bob = new Person("Bob");
	  
	  delete bob;
	  bob = nullptr;
	  
	  return 0;
  }
  ```
## Abstract Classes
- It's sole purpose is for other classes to be derived from it; it acts as a blueprint for other classes
- A class becomes an abstract class once a pure virtual method is declared inside of it
	- A pure virtual method is of the form `virtual void <func_name> = 0;`. A class with a pure virtual function is an abstract class and as such, an object can not be instantiated from it
	- This contrasts with a virtual method, which is of the form `virtual void <func_name> {<code}`. With a virtual method, a class is not an abstract class as an object can still be instantiated. The user may or may not choose to override the function
- Example
	- ```c++
	  #include <iostream>
	  
	  // Here, we have an abstract class
	  class Employee {
	  private:
		  int age;
	  public:
		  void stateAge() {
			  std::cout << age; 
		  }
		  void setNewAge(int age) {
			  this->age = age;
			  // "this" refers to the object itself
		  }
		  
		  virtual void work() = 0;
		  
		  Employee(int age)
			  : age(age) {}
	  };
	  
	  class SoftwareEngineer : public Employee {
	  public:
		  void work() override {
			  std::cout << "Typing code ...\n";
		  }
		  
		  SoftwareEngineer(int age)
			  : Employee(age) {}
			  // Call the parent class
	  };
	  
	  int main(void) {
		  return 0;
	  }
	  ```
	- We must specify how much of the parent class we want to access and any pure virtual function must be overriden
		- In other words, we override the abstract template and create our own function
	- Only the constructor has to be copied and virtual functions must be overridden
## Inheritance
- If we want to rewrite a function, the method in the parent function must be marked as `virtual`
- Normally a class can be derived from any class
	- However, if we want to block that, we can add the `final` keyword
	- E.g.
		- ```c++
		  class Employee final {
			  <code>
		  }
		  ```
- `static`
	- When applied to a variable, ensures all objects under a class share the same variable
- We can inherit from classes and interfaces as such:
	- ```cpp
	  #include <string>
	  
	  class A {
	  private:
		  const int number;
		  
	  public:
		  A(const int x) : number(x) {}
		  
		  int getNumber() {
			  return number;
		  }
	  };
	  
	  class B : public A {
	  private:
		  const std::string string;
		  
	  public:
		  B(const int a, const std::string input) : A(a), string(input) {}
		  
		  std::string getString() {
			  return string;
		  }
	  };
	  ```
### Visiblity Modes
- When you inherit, you can inherit with three visibility modes:
	- `private`:
		- Members will become private
	- `protected`:
		- Members will be capped at a protected level
		- Public members will be changed to protected level
	- `public`:
		- Members retain the same visibility
- If a visibility mode is not specified, `private` mode will be used by default
- The visibility mode is specified right before specifying the parent class:
	- ```cpp
	  #include <string>
	  
	  class A {
	  private:
		  const int number;
		  
	  public:
		  A(const int x) : number(x) {}
		  
		  int getNumber() {
			  return number;
		  }
	  };
	  
	  class B : public A { // Here
	  private:
		  const std::string string;
		  
	  public:
		  B(const int a, const std::string input) : A(a), string(input) {}
		  
		  std::string getString() {
			  return string;
		  }
	  };
	  ```
## Polymorphism
- The method must be either a virtual or pure virtual method in the base class
- Use of the `override` keyword is not required, but highly encouraged for best practice
- ```cpp
  #include <string>
  
  class Animal {
  public:
	  virtual std::string sound() {
		  return "";
	  }
  };
  
  class Dog : public Animal {
  public:
	  std::string sound() override {
		  return "Woof.";
	  }
  };
  ```
### vTables & vPointers
- In order for C++ to provide polymorphism, a virtual table is required
- This is because due to the fact objects can mix and match between various actual and apparent types, types may end up being decided at runtime:
	- ```cpp
	  #include <iostream>
	  #include <string>
	  
	  class Animal {
	  public:
		  virtual std::string sound() {
			  return "";
		  }
	  };
	  
	  class Dog : public Animal {
	  public:
		  std::string sound() override {
			  return "Woof.";
		  }
	  };
	  
	  int main(void) {
		  int dynamic_type = 1;
		  
		  Animal* animal = (dynamic_type == 0) ? new Animal() : new Dog();
		  
		  std::cout << animal->sound() << '\n';
		  
		  return 0;
	  }
	  ```
## Destructors
- The opposite of a constructor; when a class goes out of scope, its default destructor calls the destructors of smart members such as `std::string` or `std::unique_ptr` to clear their heap memory, in preperation for the members to fall off the stack. However, a default destructor does not have the ability to clear heap memory itself. As such, if there's a raw pointer in a class, a default destructor will not clear the heap memory, and there'll be a memory leak
- However, we do not want to write our own destructors, usually, as we do not want to manually manage memory. Instead, we usually use smart pointers and more modern memory management
- The only time one should write a destructor is for the top-most parent class of a tree of derivations. In such a case, one should write `virtual ~<class_name>() = default;`. Due to the `virtual` keyword, C++ will now try to find the destructors of any derived classes and call their destructors. Without it, if we upcast, which is treating a child object as a parent object for generality, if we try to destroy it as it is, the parent class destructor will be called, but not the child class. Additionally, if the top-most parent class destructor is virtual, all the destructors in the child classes become virtual
## `explicit` Keyword
### Sources
- [Geeks for Geeks](https://www.geeksforgeeks.org/cpp/use-of-explicit-keyword-in-cpp/)
# Error Handling
- [[#`<expected>` Header]]
- [[#`<optional>` Header]]
## Exceptions
- [[Libraries (C++) (CPP)#`<stdexcept>` Header|Here]]
# Templates
## Sources
- [Geeks for Geeks](https://www.geeksforgeeks.org/cpp/templates-cpp/)
- [Wikipedia - CRTP](https://en.wikipedia.org/wiki/Curiously_recurring_template_pattern)
- [CPP Reference - CRTP](https://en.cppreference.com/cpp/language/crtp)
## Introduction
- We can abstractly define a function, struct, or class that takes `<typename T>` type. In others words, we can make a blueprint for a class or functiont that can take in any type
## Curiously Recurring Template Pattern (CRTP)
- Where a class `X` derives from a class template `Y`, which takes in a template parameter `Z`, and where `Y` is instantiated with `Z = X`:
	- ```cpp
	  template <typename Z>
	  class Y {};
	  
	  class X : public Y<Z> {};
	  ```
- CRTP can be used to implement static polymorphism
	- ```cpp
	  template <typename Derived>
	  class EigenBase {
	  public:
		  /** We specifically used the implementation specified by Derived */
		  int getCols() {
			  return static_cast<Derived*>(this)->getCols();
		  }
		  
		  int getRows() {
			  return static_cast<Derived*>(this)->getRows();
		  }
	  };
	  
	  class Matrix : public EigenBase<Matrix> {
	  private:
		  int cols;
		  int rows;
		  
	  public:
		  Matrix(int cols, int rows) : cols(cols), rows(rows) {}
		  
		  int getCols() {
			  return cols;
		  }
		  
		  int getRows() {
			  return rows;
		  }
	  };
	  
	  template <typename Derived>
	  class Transpose : public EigenBase<Transpose<Derived>> {
	  private:
		  Derived& derived;
		  
	  public:
		  Transpose(Derived& derived) : derived(derived) {}
		  
		  int getCols() {
			  return derived.getRows();
		  }
		  
		  int getRows() {
			  return derived.getCols();
		  }
	  };
	  
	  template <typename Derived>
	  void printDimensions(EigenBase<Derived>& derived) {
		  std::cout << "I have " << derived.getCols() << " columns and " << derived.getRows() << " rows.\n";
	  }
	  
	  int main(void) {
		  Matrix* matrix = new Matrix(6, 7);
		  Transpose<Matrix>* transpose = new Transpose<Matrix>(matrix);
		  
		  printDimensions(*matrix); // Dereference the pointers
		  printDimensins(*transpose);
		  
		  delete matrix;
		  matrix = nullptr;
		  delete transpose;
		  transpose = nullptr
	  }
	  ```
	- Here, we can call `getCols()` and `getRows()` generically in `printDimension()` but each class uses their custom implementation of it
	- Note `EigenBase` should not be treated like a traditional runtime interface
	- Apparent and actual types should be the same
## Examples
- Initialization as a function
	- ```c++
	  template <typename T>
	  T sum(T a, T b) {
		  return a + b;
	  }
	  ```
- Initialization as a struct
	- ```c++
	  template <typename T>
	  struct ThreeThings {
		  T one;
		  T two;
		  T three;
	  };
	  ```
- Initialization as a class
	- ```c++
	  template <typename T>
	  class Box {
	  private:
		  T item;
	  public:
		  void replaceItem(T new_item) {
			  this->item = new_item;
		  }
		  
		  T getItem() {
			  return this->item;
		  }
	  };
	  ```
# Namespaces
- They act as folders to help organise things
	- This way, we can have functions that are exactly the same, which overloading can not solve
- Nestable
- Initialization
	- ```c++
	  namespace car {
		  void move(int distance) {
			  // car specific movement
		  }
	  }
	  
	  namespace bicycle {
		  void move(int distance) {
			  // bicycle specific movement
		  }
	  }
	  ```
# Modularity
## `extern` Keyword
### Sources
- [Geeks for Geeks - How to Use extern](https://www.geeksforgeeks.org/cpp/how-do-i-use-extern-to-share-variables-between-c-source-files/)
### Introduction
- !!!
### Usage
- !!!
## Header Files
### Introduction
- To make it easier to manage a multifile system, we can use header files, with a `.hpp` extension
- In a header file, we write signatures for functions and classes in the respective `.cpp` file. This is so we can simply include the header file in `main.cpp` to attain the functionality of the other `.cpp` files. How it works is that in order for `main.cpp` to compile with the functionality of the other files, the bare minimum required are the signatures. In a way, this is appeasing to the compiler. This is contrasted to simply including the `.cpp` file, which would lead to the compiler literally copy pasting all the code in the external file to `main` behind the scenes, which would get quite slow with a lot of external files
- But you may ask: how does C++ find the functionality of the files, you just said they get the signatures, a signature has no functionality. That's where [[#Linking|linkers]] come in
### Using Header Files
- Generally, each `.cpp` file should have a `.hpp` file, outside of `main` of course
- The relative locations of `.cpp` and `.hpp` files does not matter, as long as they are within the root directory
- It is a good practice to group `.hpp` files and `.cpp` files
- We always write `#pragma once` at the top of a header file. This is because, sometimes, we need to put header files in header files, as functions rely on each other. In such a scenario, the header files can see each other. Without `#pragma once`, redefinitions will occur
- We include as `"<helper>.hpp"`. Quotations are for project folders files and angle brackets are for system files
- Sometimes we need to include standard libraries in the header files so they can understand, for example, what `std::vector` means
- We might use header files as such; we will assume they are all in the same directory
	- `helper.cpp`
		- ```c++
		  #include "helper.hpp"
		  
		  int sum(int a, int b) {
			  return a + b;
		  }
		  ```
	- `helper.hpp`
		- ```c++
		  #pragma once
		  
		  int sum(int a, int b);
		  ```
	- `main.cpp`
		- ```c++
		  #include "helper.hpp"
		  
		  #include <iostream>
		  
		  int main(void) {
			  int a = 1;
			  int b = 2;
			  
			  std::cout << "The sum is: " << sum(a, b) << '\n';
			  
			  return 0;
		  }
		  ```
- For classes, we write out the interface in the `.hpp` file and the implementation of the methods in the `.cpp` file:
	- `.hpp`:
		- ```c++
		  #pragma once
		  
		  class Helper {
		  private:
			  static constexpr int SomeGlobal = 0;
			  
		  public:
			  static void entryPointA();
			  
			  void entryPointB();
		  private:
			  static int helper();
		  }
		  ```
	- `.cpp`:
		- ```c++
		  #include "helper.hpp"
		  
		  void Helper::entryPointA() {
			  // Stub
		  }
		  
		  void Helper::entryPointB() {
			  // Stub
		  }
		  
		  int Helper::helper() {
			  // Stub
		  }
		  ```
			- Doesn't matter if it's static or not, do not write static
			- And we use `::` the same, regardless
## Linking
- Linking is where the real magic happens
- Nowadays, linking is handled by third party tools, such as [[Build Tools (C++) (CPP)#CMake|CMake]]
- When a linker is called, when needed it fetches the code from the appropriate `.o` files, which were compiled correctly with the appropirate header files to "fill in the signatures"
- To link via the command line, simply include the needed `.cpp` files
	- E.g. `clang++ -o main main.cpp helper.cpp`
## Including Files in Different Directories
- If we want to include headers across the directory, we type the same things in our files, but we use a different compile statement
- We have to include the tag `-I` immediately followed by the folder, with no space, that we want the compiler to search for header files
	- If we need to search multiple files, we use multiple instances of this strategy
- However, this search is not recursive; the compiler will only search the immediate directory given
- E.g.
	- Suppose we have a `source` directory and a `console` directory with the main logic functions in the `source` directory and the `main.c` entry file in the `console` directory. For the compiler to know where to look for the header files, we would have to write something like `clang++ -I./source -o main main.cpp ...`
	- If we had two directories in `source` such as `logic` and `persistence` in `source`, then we would have to write `clang++ -I./logic -I./persistence -o main main.cpp ...`
- A more preferable and professional strategy altogether would be use a [[Projects (C++) (CPP)#Building|build tool]]
## Include Order
1. Respective [[#Header Files|header file]]
2. [[Core (C)]] headers
3. [[#Standard Library (STL)|Standard library]] headers
4. Third party headers
5. Other header files
# Libraries
## Header Only
### Sources
- [Wikipedia](https://en.wikipedia.org/wiki/Header-only)
### Introduction
- !!!
# Named Requirements
## Sources
- [CPP Reference - Named Requirements](https://en.cppreference.com/cpp/named_req)
## Introduction
- !!!
## BitmaskType
- !!!
## Callable
- !!!
## CopyAssignable
- !!!
## CopyConstructible
- !!!
## FunctionObject
- !!!
## MoveConstructible
- !!!
## UnformattedInputFunction
- !!!
## UnformattedOutputFunction
- !!!
