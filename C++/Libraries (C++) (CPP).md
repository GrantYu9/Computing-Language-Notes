# Standard Library (STL)
- `std::erase(<container>, <value>)`
	- Searches and removes all values in a container
- `std::erase_if(<container>, <condition>)`
	- Removes if condition is met
	- Like `filter` from Racket in [[CPSC - 110 - Computation, Programs, and Programming|CPSC 110]]
## `<algorithm>` Header
- `std::all_of(<beginning_iterator>, <end_iterator>, <function>)`
	- Returns a `bool`
	- Check if all items satisfy the condition as a function
- `std::any_of(<beginning_iterator>, <end_iterator>, <function>)`
	- Returns a `bool`
	- Checks if $\exists$ an item that satisfies the condition as a function
- `<data_structure>.begin()`
	- Returns an iterator to the first element of the data structure
- `std::binary_search(<beginning>, <end>, <value_you_want_to_search_for>)`
	- Returns a boolean
- `<data_structure>.end()`
	- Returns an iterator to where the next element would be written in memory
- `std::count_if(<beginning_iterator>, <end_iterator>, <function>)`
- `std::find_if(<start_iterator>, <end_iterator>, <function>)`
- `std::for_each(<beginning_iterator>, <end_iterator>, <function>)`
- `std::lower_bound(<iterator_beginning>, <iterator_end>, <target>)`
	- Returns iterator to first element $\ge$ `target`
- `std::max(<values>)`
- `std::min(<values>)`
- `std::none_of(<beginning_iterator>, <end_iterator>, <function>)`
	- Returns `bool`
	- Checks if none of the items satisfy the condition, as a function
- `std::reverse(<iterator_start>, <iterator_end>);`
	- Reverses a container
- `std::sort(<beginning>, <end>, <lambda_expression>)`
	- Works on all sorts of data structures
		- [[Arrays]]
		- [[Linked Lists]]
	- In order to generically work on various types of data structures, one needs to pass in the beginning and end of the container, via the `.begin()` and `.end()` methods
	- Uses an optimized mix of sorts in an attempt to achieve $O(n\log n)$ runtime
	- !!!
- `std::swap(<element1>, <element2>)`
	-  Swaps two elements in an array
- `std::upper_bound(<iterator_beginning>, <iterator_end>, <int_target>)`
	- Uses binary search to return an iterator to the first element $>$ `target`
- `<array>.size()`
	- Returns the size of the array
- `std::transform`
	- !!!
## `<any>` Header
### Sources
- [CPP Referenc](https://en.cppreference.com/cpp/header/any)
### Introduction
- !!!
### Classes
#### `any` Class
##### Introduction
- `class any;`
##### Initialization
- ```cpp
  template <class ValueType>
  any(ValueType&& value);
  ```
	- !!!
## `<array>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/container/array)
### Introduction
- !!!
### Classes
#### `array` Class
##### Introduction
- `std::array` is stack allocated, as opposed to `std::vector`, which is heap allocated
- ```cpp
  template<class T, std::size_t N>
  struct array
  ```
##### Initialization
- `std::array< <data_type>, <size> > <name> = {<values>};`
	- Fixed size and state
##### Methods
- `<array>[<index>];`
	- Returns element at index without bounds checking
- `<array>.at(<index>);`
	- Returns element at index with bounds checking
- `<array>.back();`
	- Returns last element
- `<array>.begin();`
- `<array>.data();`
	- Returns raw pointer of the array
- `<array>.empty();`
	- Returns true if array is of size $0$
- `<array>.end();`
- `<array>.fill(<value>);`
	- Fills all entries with `<value>`
- `<array>.front();`
	- Returns first element
- `<array>.size();`
## `<chrono>` Header
- `std::chrono::steady_clock`
	- Internal clock
- `std::chrono::system_clock`
	- Clock based on real world time
- `std::this_thread::sleep_until(time_point)`
	- Pauses program until a time point
- `std::chrono::duration_cast< <type> >(<variable>)`
	- Type cast
- `std::chrono::<clock_type>::now()`
	- Returns the current time
- `<time_variable>.count()`
	- Returns the value without units
### Data Types
- `std::chrono::<clock_type>::time_point`
- `std::chrono::nanoseconds <name>(<value>);`
- `std::chrono::microseconds <name>(<value>);`
- `std::chrono::milliseconds <name>(<value>);`
- `std::chrono::seconds <name>(<value>);`
- `std::chrono::minutes <name>(<value>);`
- `std::chrono::hours <name>(<value>);`
- `std::chrono::days <name>{<value>};`
- `std::chrono::weeks <name>{<value>};`
- `std::chrono::months <name>{<value>};`
- `std::chrono::years <name>(<value>);`
## `<cassert>` Header
### Sources
- [Geeks for Geeks](https://www.geeksforgeeks.org/cpp/assertions-cc/)
- [CPP Reference](https://en.cppreference.com/cpp/error/assert)
### Introduction
- !!!
### Macros
- `#define assert(<condition>)`
## `<cmath>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/cmath)
### Introduction
- Support for extended math operations
### Functions
- `float abs(float num)`
	- Until C++23
	- Takes the absolute value of `num`
- `std::ceil(<number>)`
	- [[Functions#Ceiling Function|Ceiling]]
- `double exp(double num)` and `float exp(float num)`
	- $e^\text{num}$
- `std::floor(<number>)`
	- [[Functions#Floor Function|Floor]]
- `float log(float num)`
	- Until C++23
	- Returns the natural logarithm of `num` 
- `std::pow(<number_1>, <number_2>)`
	- Big warning, this does floating point computations!
- `float sqrt(float num)`
	- Until C++23
	- Computes square root of `num`
## `<cstddef>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/cstddef)
### Introduction
- !!!
### Types
- `size_t`
	- !!!
## `<cstdint>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/cstdint)
### Introduction
- Provides precise primitive types
### Types
- `int8_t`
	- 1 byte
	- Signed
- `uint8_t`
	- 1 byte
	- Unsigned
- `int16_t`
	- 2 bytes
	- Signed
- `uint16_t`
	- 2 bytes
	- Unsigned
- `int32_t`
	- 4 bytes
	- Signed
- `uint32_t`
	- 4 bytes
	- Unsigned
- `int64_t`
	- 8 bytes
	- Signed
- `uint64_t`
	- 8 bytes
	- Unsigned
## `<deque>` Header
- Double ended queue
- `std::deque<data_type> <name> = {<values>};
### Methods
- `<deque>[<index>];`
	- Access index without bounds checking
- `<deque>.at(<index>);`
	- Access index with bounds checking
- `<deque>.clear();`
	- Clears the deque
- `<deque>.empty();`
	- Returns true if the deque is empty
- `<deque>.front();`
	- Returns first element
- `<deque>.back();`
	- Returns last element
- `<deque>.pop_back();`
	- Removes last element
- `<deque>.pop_front();`
	- Removes first element
- `<deque>.push_back(<value>);`
	- Adds a value to the end
- `<deque>.push_front(<value>);`
	- Adds a value to the front
- `<deque>.resize(<value>);`
	- Changes deque size to `<value>`
- `<deque>.size();`
## `<exception>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/exception)
### Introduction
- !!!
### Classes
#### `exception` Class
##### Methods
- `virtual const char* what() const noexcept`
	- Returns the explanatory string
## `<expected>` Header
- `std::expected`
	- Used when we need to return an explanation for an error
		- E.g. Hm, my mail is not in box. It's been over a day and the mailman is usually not that late, perhaps someone stole it. Who was it and when?
	- Can return more complex error outputs than [[#`<optional>` Header]]
	- ```c++
	  std::expected< <expected_value>, <error_output_type> > <function_name>(<parameters>) {
		  // stub
	  }
	  ```
## `<filesystem>` Header
### Sources
-  [Geeks for Geeks](https://www.geeksforgeeks.org/cpp/file-system-library-in-cpp-17/)
- [CPPReference](https://en.cppreference.com/cpp/filesystem)
### Introduction
- Provides implementation to operate on a filesystem
### Functions
- `std::uintmax_t file_size(const std::filesystem::path& p)`
	- If `p` does not exist, report an error
	- Returns size of `p`
- `bool is_empty(const std::filesystem::path& p)`
	- Checks whether `p` is an empty file, or directory
### Classes
#### `path` Class
##### Introduction
- Represents a path
##### Initialization
- `path(const path& path)`
- `path(string_type&& source, format fmt = auto_format);
##### Attributes
- `value_type`
	- Character type used by the local operating system
		- `char` on POSIX
		- `wchar_t` on Windows
##### Methods
- `template<class Source> path& append(const Source& source)`, `path& operator/=(const path& p)`, or `template<class Source> path& operator/=(const Source& source)`
	- Appends a file path to a file path
	- You can pass in strings to paths
- `path parent_path() const`
	- Returns path of the parent directory
- `std::string string() const`
	- Return the path as a string
## `<format>` Header
- !!!
## `<forward_list>` Header
- Singly linked list
- `std::forward_list<data_type> <name> = {<values>};`
### Methods
- `<forward_list>.begin()`
	- Iterator to the first element
- `<forward_list>.before_begin()`
	- Returns an iterator to the space before the first element
- `<forward_list>.clear()`
	- Destroys all elements
- `<forward_list>.end()`
	- Iterator to space after last element
- `<forward_list>.erase_after(<iterator>)`
	- Removes element after iterator
- `<forward_list>.front()`
	- Returns a reference to the first element
- `<forward_list>.insert_after(<iterator>, <value>)`
	- Adds value in position after iterator
- `<forward_list>.pop_front()`
	- Removes first element
- `<forward_list>.push_front(<value>)`
	- Adds an element to the beginning
- `<forward_list>.remove(<value>)`
	- Removes all instances of `<value>`
- `<forward_list>.remove_if(<condition>)`
	- Removes if the condition is satisfied
- `<forward_list>.reverse()`
	- Reverses the list
- `<forward_list>.sort()`
- `<forward_list>.splice_after(<iterator>, <other_list>)`
	- Appends `<other_list>` to position right after `<iterator>`
- `<forward_list>.unique()`
	- Removes consecutive duplicate elements
## `<fstream>` Header
- Used to read and write to files from the system
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/fstream)
### Introduction
- !!!
### Classes
#### `basic_ifstream` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>
  class basic_fstream : public std::basic_istream<CharT, Traits>;
  ```
- Inherits from [[#`basic_istream` Class|basic_istream]]
- Support for input streams specialized for files
##### Initialization
- `explicit basic_ifstream(const char* filename, std::ios_base::openmode mode = std::ios_base::in)`
- `explicit basic_ifstream(const std::filesystem::path::value_type* filename, std::ios_base::openmode mode = std::ios_base::in)`
- `explicit basic_ifstream(const std::string& filename, std::ios_base::openmode mode = std::ios_base::in)`
##### Typedefs
- `typedef std::basic_ifstream<char> std::ifstream`
#### `basic_ofstream` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_ofstream : public std::basic_ostream<CharT, Traits>;
  ```
- Inherits from [[#`basic_ostream` Class|basic_ostream]]
- Support for output streams specialized for files
##### Initialization
- `explicit basic_ofstream(const char* filename, std::ios_base::openmode mode = std::ios_base::out)`
- `explicit basic_ofstream(const std::filesystem::path::value_type* filename, std::ios_base::openmode mode = std::ios_base::out)`
- `explicit basic_ofstream(const std::string& filename, std::ios_base::openmode mode = std::ios_base::out)`
##### Methods
- `void close`
	- Closes the associated file
- `open`
	- `void open(const char* filename, std::ios_base::openmode mode = std::is_base::out)`
	- `void open(const std::string& filename, std::ios_base::openmode mode = std::is_base::out)`
	- `void open(const std::filesystem::path& filename, std::ios_base::openmode mode = std::is_base::out)`
	- Opens a file and associates it with the stream
##### Typedefs
- `typedef std::basic_ofstream<char> std::ofstream`
#### `basic_fstream` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_fstream : public std::basic_iostream<CharT, Traits>;
  ```
- Inherits from [[#`basic_iostream` Class|basic_iostream]]
- Support for input and output streams specialized for files
##### Initialization
- `explicit basic_fstream(const char* filename, std::ios_base::openmode mode = std::ios_base::out | std::ios_base::out)`
- `explicit basic_fstream(const std::filesystem::path::value_type* filename, std::ios_base::openmode mode = std::ios_base::out | std::ios_base::out)`
- `explicit basic_fstream(const std::string& filename, std::ios_base::openmode mode = std::ios_base::out | std::ios_base::out)`
### General
- `<file>.is_open();`
	- Checks if the file is open
- `<file>.open();`
	- Opens the file
- `<file>.close();`
	- Closes the file
- C++ will automatically try to find files and make files in the current directory, which may change depending on where execution happens
	- E.g. `std::ofstream out_file("this.txt");` will make a text file in the current directory
- Any stream type will open a file, but according to its own rules
### `std::ofstream` (Colour)
- For writing
- Allows us to create a file
- ```c++
  #include <fstream>
  #include <iostream>
	  
  int main(void) {
	  // Creates "file" with some text, and "std::ios::app" means we can append
	  // text when we try to write
	  // Without "std::ios::app", "std::ofstream" will be overwrite by default
	  std::ofstream file("Hello world!\n", std::ios::app);
	  
	  if (file) {
		  file << "Some appended text\n";
		  file.close(); // Always close the file
	  }
  }
  ```
### `std::ifstream` (Colour)
- For reading
- ```c++
  #include <fstream>
  #include <iostream>
  #include <string>
  
  int main(void) {
	  std::ifstream file("data.txt"); // Looks for this file
	  
	  std::string line; // We need to initialize this
	  
	  if (file) {
		  while (std::getline(file, line)) {
			  std::cout << "Line: " << line << '\n';
		  }
	  }
  }
  ```
- `std::getline` also needs [[#`<string>` Header]]
	- `std::getline(<stream>, <string>, <delimiter>);`
		- Reads until `<delimiter>` is hit
		- By default, it's  `\n`
### `std::fstream` (Colour)
- Read and write
## `<functional>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/functional)
### Introduction
- !!!
### Classes
#### `function` Class
##### Introduction
- ```cpp
  template <class>
  class function;
  ```
- ```cpp
  template <class R, class ... Args>
  class function<R(Args ...)>;
  ```
##### Initialization
- `function() noexcept`
	- !!!
- `function(const function& other)`
	- !!!
- `function(function&& other)`
	- !!!
- `template <class F> function(F&& f)`
	- Initializes with `std::forward<F>(f)` and of type `std::decay<F>::type`
	- An lvalue of type `std::decay<F>::type` is callable for argument types `Args ...` and if it is possible to return type `R`
#### `hash` Class
- `std::hash`
	- `std::hash<T>{}(<int_value>)`
	- !!!
## `<ios>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/ios)
### Introduction
- !!!
### Classes
#### `basic_ios` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_ios : public std::ios_base;
  ```
- Provides support for interfacing with objects that have a [[#`basic_streambuf` Class|basic_streambuf]] interface
##### Methods
- `bool eof() const`
	- Returns `true` if associated stream has reached end of file
- `bool operator!() const`
	- Returns true if an error has occured in the associated stream
- `std::basic_streambuf<CharT, Traits>* rdbuf() const`
	- Return the associated stream buffer. Else, return `nullptr`
#### `ios` Class
- !!!
#### `ios_base` Class
##### Introduction
- The base class for all IO stream classes
- !!!
##### Attributes
- `typedef T4 seekdir`
	- Specifies file seeking direction type
	- `static constexpr seekdir beg = /** Hidden implementation */`
		- Beginning of stream
	- `static constexpr seekdir end = /** Hidden implementation */`
		- End of stream
	- `static constexpr seekdir cur = /** Hidden implementation */`
		- Current position of stream indicator
##### Typedefs
- `typedef unsigned int openmode`
	- A [[Core (C++) (CPP)#BitmaskType|BitmaskType]]
	- `static const openmode binary = 0x04`
	- `static const openmode in = 0x08`
	- `static const openmode out = 0x10`
	- `static const openmode trunc = 0x20`
#### `streamsize` Class
- Represents the number of characters transferred in an I/O operation or the size of an I/O buffer
- `typedef <implementatino> streamsize;
## `<iostream>` Header
- `std::cout << <stuff>;`
- `std::cin >> <stuff>;`
- `std::cerr << <stuff>;`
	- Unbuffered, sends data to screen immediately
	- For critical error messages
## `<iomanip>` Header
- `std::scientific`
	- Modifies the output to print numbers in scientific format
	- Example with `std::setprecsion()`
		- ```cpp
		  #include <iostream>
		  #include <iomanip>
		  
		  int main(void) {
			  double x = 1.0;
			  
			  std::cout << std::scientific << std::setprecision(2) << x << '\n';
			  
			  return 0; 
		  }
		  ```
- `std::setprecision(<natural_number>)`
	- Pass in a natural number to $\dots$ for the precision
	- Max precision for a double in ARM system is 17 digits
	- Example
		- ```cpp
		  #include <iostream>
		  #include <iomanip>
		  
		  int main(void) {
			  double x = 1.0;
			  
			  std::cout << std::setprecision(2) << x << '\n';
			  
			  return 0; 
		  }
		  ```
		  - Output would be 1.00
## `<istream>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/istream)
### Introduction
- !!!
### Classes
#### `basic_istream` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_istream : virtual public std::basic_ios<CharT, Traits>;
  ```
 - Inherits from [[#`basic_ios` Class|basic_ios]] 
  - Provides high level specialized support for input operations on character streams
##### Methods
- `std::streamsize gcount() const`
	- Returns size of bytes read for last read operation
- `get`
	- !!!
- `int_type peek()`
	- !!!
- `pos_type tellg()`
	- !!!
- `basic_istream& read(char_type* s, std::streamsize count)`
	- Reads characters from stream and store to `s`
- `basic_istream& seekg(pos_type pos)` or `basic_istream& seekg(off_type off, std::ios_base::seekdir dir)`
	- Sets input position reader to `pos`
#### `basic_iostream` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_iostream: public basic_istream<CharT, Traits>, public basic_ostream<CharT>, Traits>>;
  ```
- Inherits from
	- [[#`basic_istream` Class|basic_istream]]
	- [[#`basic_ostream` Class|basic_ostream]]
## `<iterator>` Header
- `std::advance(<iterator>, <number_of_steps>);`
	- Moves the iterator a certain amount of steps forward
- `std::distance(<iterator1>, <iterator2>);`
	- Distnace between two iterators
- `std::next(<iterator>, <steps>);`
	- If no steps, it will just increment
	- Does not modify the iterator
- `std::prev(<iterator>, <steps>)`
	- If no steps, it will just decrement
	- Does not modify the iterator
## `<list>` Header
- `std::list< <data_type(s)> > <name> {<element(s)>};
	- [[Linked Lists#Doubly Linked|Doubly linked list]]
### Methods
- `<list>.back();`
	- Returns the last element
- `<list>.front();`
	- Returns the first element
- `<list>.pop_back();
	- Remove from back
- `<list>.pop_front();`
	- Remove from front
- `<list>.push_back(<element>);`
	- Add to back
- `<list>.push_front(<element>);`
	- Add to front
- `<list>.size();`
- `<destination_list>.splice(<destination>, <source_list> ,<source>);`
	- Where `<destination>` and `<source>` are iterators in their respective lists
	- Allows one to move contents from a list to another, to and from wherever they chose
## `<map>` Header
- `std::map< <data_type_1>, <data_type_2> >`
	- [[Trees#Red-Black Tree|Red-black tree]]
- !!!
## `<memory>` Header
- `->` and `*` work as per usually when trying to access what the pointer is pointing to
### `std::unique_ptr` Type
- A pointer that enforces it is the only pointer that points to an object
	- "There can be only one!"
#### Initialization
- `std::unique_ptr <data_type>(<target_data_type>);`
- `auto <name> = std::make_unique<data_type>(<data_type_constructor_operands>);`
#### Methods
- `<unique_ptr>.get()`
	- Returns the raw pointer
### `std::shared_ptr` Type
- `auto <name> = std::make_shared<data_type>();`
	- Initialization
- A pointer that may be among many that point to an object
- `<smart_ptr>.use_count();`
	- Returns number of pointers pointing to the same object
### `std::weak_ptr` Type
- `std::weak_ptr<int> <name> = <object_observed_by_unique_ptr>`
	- Initialization
- A pointer that can only observe objects
	- Well, it can't even observe, as it can not even read contents
- `<weak_ptr>.lock()`
	- Attempts to cast the weak pointer into a unique pointer
	- If succesful, returns the unique pointer. If not, returns `nullptr`
- `<weak_ptr>.expired();`
	- Checks if the object is dead
## `<numeric>` Header
- `std::accumulate`
	- !!!
- `std::gcd`
	- !!!
## `<optional>` Header
- C++17
- `std::optional`
	- Used to check whether a values exists or not. If the value does not exist, that's perfectly fine
		- E.g. Is my mail in my mailbox? No? That's fine, sometimes it comes late and it's a little early right now
	- Gives a boolean output; it's either there or it's not
	- `std::optional< <data_type> > <name>;`
	- ```c++
	  std::optional< <expected_data_type> <function_name>(<parameters>) {
		  if (<condition>) return <output>; // If it works
		  return std::nullopt; // If it fails
	  }
	  ```
	- E.g.
		- ```c++
		  #include <iostream> 
		  #include <optional>
		  
		  int main(void) {
			  std::optional<int> number;
			  
			  if (!number) { // We check if it has a value
				  std::cout << "Uh oh, it has no value!" << '\n';
				  return 1;
			  }
			  
			  std::cout << "The number is: " << number << ".\n";
			  
			  return 0;
		  }
		  ```
- `std::nullopt`
	- A fancy `NULL`, which is a class
	- Can be treated as a data type
### Methods
- `<optional_type>.hasvalue()`
	- Checks if the optional type returns a value
- `<optional_type>.value()`
	- Returns the value
- `<optional_type>.value_or(<error_output>)`
	- Returns a value or returns something as an output upon `std::nullopt`
## `<ostream>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/ostream)
### Introduction
- !!!
### Classes
#### `basic_ostream` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_ostream : virtual public std::basic_ios<CharT, Traits>;
  ```
- Inherits from [[#`basic_ios` Class|basic_ios]]
- Provides higher level specialized support for output character streams
##### Methods
 - `basic_ostream& seekp(pos_type pos)`
	 - Positions indicator `pos` bytes relative to the beginning
 - `basic_ostream& seekp(off_type off, std::ios_base::seekdir dir)`
	 - Positions indicator `off` bytes relative to `dir`
- `basic_ostream& write(const char_type* s, std::streamsize count)`
	- Inserts `<s>` into the file
	- Returns `*this`
## `<print>` Header
- `std::print(<string>);`
	- Works like [[Core (Python)]]
	- E.g. `std::print("The sum of {} and {} is {}", x, y, x+y);`
- `std::println(<string>);`
	- Newline
## `<queue>` Header
- `std::queue< <data_types(s)> > <name>;
	- You can not initialize `std::queue` with values in it
### Methods
- `<queue>.empty()`
	- Returns `bool` informing us whether the queue is empty or not
- `<queue>.front()`
	- Returns the first element
- `<queue>.pop();`
	- Removes the first element
- `<queue>.push(<element>);`
	- Adds an element to the end
- `<queue>.size();`
## `<random>` Header

### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/random)
### Introduction
- Offers support for psuedorandom number generators across various contexts
- Generally the workflow is
	- Use a non deterministic random number generator to create a seed. E.g. `random_device`
	- Pass the seed to a deterministic random number generator. E.g. `mersenne_twister_engine`
	- Optionally pass it to other generators. E.g. `uniform_real_distribution`
- The header splits up many of the classes to make each component as lightweight as possible and allow easy reusability
	- For example, we may use the `mt19937` generator for several types of distributions. This way we can avoid duplicating heavy implementation details for generators in each distribution type
	- Furthermore, some parts are much heavier than others and it would be highly advantageous to represent them as standalone classes. For example, `random_device` is a tool that uses machine entropy to create non-deterministic numbers. However, this is quite a heavy operation as it requires IO bound tasks such as system interrupts and waiting for IO calls. As such, it would make sense to use it just once to create a seed and use a deterministic generator to generate the numbers
### Classes
#### `mersenne_twister_engine` Class
##### Introduction
- ```cpp
  template<class UIntType, std::size_t w, std::size_t n, std::size_t m, std::size_t r, UIntType a, std::size_t u, UIntType d, std::size_t s, UIntType b, std::size_t t, UIntType c, std::size_t l, UIntType f>
  class mersenne_twister_engine
  ```
- !!!
##### Methods
- !!!
#### `random_device` Class
##### Introduction
- !!!
#### `uniform_int_distribution` Class
##### Introduction
- !!!
#### `uniform_real_distribution` Class
##### Introduction
- !!!
### Typedefs
- `typedef std::mersenne_twister_engine<std::uint_fast32_t, 32, 624, 397, 31, 0x9908b0df, 11, 0xffffffff, 7, 0x9d2c5680, 15, 0xefc60000, 18, 1812433253>> mt19937`
## `<ranges>` Header
- !!!
## `<set>` Header
- `std::set< <data_type> > <name> = {<values>};
	- [[Trees#Red-Black Tree|Red-black tree]]
- !!!
## `<span>` Header
- `std::span<data_type> <name>`
	- Used to read or write containers "at a distance" without having to pass in the entire container
	- Only works on containers of continuous memory
- E.g.
	- ```c++
	  void printNumbers(std::span<int> container) {
		  for (const int i : container) {
			  std::cout << i << " \n";
		  }
	  }
	  
	  int main(void) {
		  std::array<int> array = {1, 2, 3};
		  std::vector<int> vector = {4, 5, 6};
		  
		  printNumbers(array); // Works
		  printNumbers(vector); // Also works
	  }
	  ```
## `<sstream>` Header
### Sources
- !!!
### Initialization
- `std::stringstream <name>(<std::string>);`
## `<streambuf>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/streambuf)
### Introduction
- !!!
### Classes
#### `basic_streambuf` Class
##### Introduction
- ```cpp
  template<class CharT, class Traits = std::char_traits<CharT>>
  class basic_streambuf;
  ```
- Manages the input and output buffer of a character sequence
##### Methods
- `pos_type pubseekpos(pos_type pos, std::ios_base::openmode which = std::ios_base::in | std::ios_base::out)`
	- !!!
## `<stack>` Header
- `std::stack<data_types> <name>;
	- You can not initialize `std::stack` with values in it
### Methods
- `<stack.empty()`
	- Checks whether the stack is empty or not
- `<stack>.pop()`
	- Removes the first element
- `<stack>.push(<element>)`
	- Adds an element to the front
- `<stack>.size()`
- `<stack>.top()`
	- Returns the first element
## `<stacktrace>` Header
- C++23
- !!!
## `<stdexcept>` Header
### Sources
- [Geeks for Geeks](https://www.geeksforgeeks.org/cpp/exception-handling-c/)
### Keywords
- `try`
	- Runs code as per usually, until a `throw` statement is reached, in which the program will immediately go to the next `catch` code block
- `throw`
	- "Throws" an error for `catch` to register
- `catch`
	- Attempt to "catch" an error of a certain data type. If succesfull, the code block in `catch` will run. If not, it will not run
- E.g.
	- ```c++
	  try {
		  // Some code
		  
		  throw 1;
		  
		  // More code that would not run
	  }
	
	  catch (int e) { // The type just has to be the same as the thrown exception
		  // Code that would run
	  }
	  ```
### Classes
#### `logic_error` Class
##### Introduction
- Inherits from [[#`exception` Class|exception]]
##### Initialization
- `logic_error(const std::string& message)`
- `logic_error(const char& message)`
#### `out_of_range` Class
##### Introduction
- Inherits from [[#`logic_error` Class|logic_error]]
##### Initialization
- `out_of_range(const std::string& message)`
- `out_of_range(const char& message)`
#### `overflow_error` Class
##### Introduction
- Inherits from [[#`runtime_error` Class|runtime_error]]
##### Initialization
- `runtime_error(const std::string& message)`
- `runtime_error(const char& message)`
#### `runtime_error` Class
##### Introduction
- Inherits from [[#`exception` Class|exception]]
##### Initialization
- `runtime_error(const std::string& message)`
- `runtime_error(const char& message)`
#### `underflow_error` Class
##### Introduction
- Inherits from [[#`runtime_error` Class|runtime_error]]
##### Initialization
- `underflow_error(const std::string& message)`
- `underflow_error(const char& message)`
## `<string>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/string)
### Introduction
- !!!
### Classes
#### `basic_string` Class
##### Introduction
- ```cpp
  namespace pmr {
	  template<class CharT, class Traits = std::char_traits<CharT>>
	  using basic_string = std::basic_string<CharT, Traits, std::pmr::polymorphic_allocator<CharT>>;
  }
  ```
	- Since C++17
##### Initialization
- !!!
##### Methods
- `const CharT* c_str() const`
	- Returns a pointer to the string as a null-terminated array
- `<string>.size();` !!!
- `<string>.empty();`
	- True if string has $0$ characters
- `<string>.append(<string>);`
	- Appends a string to a string
	- `+=` also works
- `<string>.substr(<position>, <length>);`
	- Extracts a substring, from `<position>` and `<length>` characters onward. If `<length>` is omitted, rest of the string will be copied
- `<string>.find(<string>);`
	- Tries to find index of first occurrence
	- If fails, returns `std::srting::npos`
- `<string>.replace(<position>, <length>, <new_string>);`
	- Replaces contents of a string
- `<string>.clear();`
	- Clears a string
##### TypeDefs
- `typedef std::basic_string<char> std::string`
## `<string_view>` Header
- !!!
## `<thread>` Header
- `std::this_thread::sleep_for(<time_duration>)`
	- Pauses program for set amount of time
- !!!
## `<tuple>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/tuple)
### Introduction
- !!!
### Classes
#### `tuple` Class
##### Introduction
- ```cpp
  template<class ... Types>
  class tuple;
  ```
##### Initialization
- `tuple(const Types&... args)`
	- !!!
- ```cpp
  template<class ... UTypes>
  tuple(UTypes&& ... args);
  ```
	- !!!
## `<type_traits>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/type_traits)
### Introduction
- !!!
### Structs
#### `add_pointer` Struct
##### Introduction
- ```cpp
  template <class T>
  struct add_pointer;
  ```
- If `T` is a reference type, then pass it as is in `type`
- Otherwise, `type` is `T*`
##### Methods
- `type`
	- Pointer to `T` or the type referenced by `T`
#### `add_lvalue_reference` Struct
##### Introduction
- ```cpp
  template <class T>
  struct add_lvalue_reference;
  ```
#### `add_rvalue_reference` Struct
##### Introduction
- ```cpp
  template <class T>
  struct add_rvalue_reference;
  ```
#### `conditional` Struct
##### Introduction
- ```cpp
  template <bool B, class T, class F>
  struct conditional;
  ```
- !!!
#### `decay` Struct
##### Introduction
- ```cpp
  template <class T>
  struct decay;
  ```
- Performs type conversions when passing arguments by value
	- If `T` is an array of `U` or a reference to it, `type` is `U*`
	- Otherwise, if `T` is a function type `F` or a reference to one, `type` is `std::add_pointer<F>::type`
	- Otherwise, `type` is `std::remove_cv<std::remove_reference<T>::type>::type`
		- So like `std::remove_cvref`
##### Attributes
- `type`
	- Result of applying decay type conversions to `T`
#### `integral_constant` Struct
##### Introduction
- ```cpp
  template <class T, T v>
  struct integral_constant;
  ```
- !!!
##### Members
- `static value`
	- !!!
#### `is_base_of` Struct
##### Introduction
- ```cpp
  template<class Base, class Derived>
  struct is_base_of;
  ```
- If `Derived` is derived from `Base` or if both are the same non-union class, provides the member constant `value = true`. Otherwise, `value = false`
##### Attributes
- `static bool value`
##### Functions
- `operator bool()`
	- Returns `value` !!!
#### `is_constructible` Struct
##### Introduction
- ```cpp
  template <class T, class ... Args>
  struct is_constructible;
  ```
- !!!
#### `is_copy_constructible` Struct
##### Introduction
- ```cpp
  template <class T>
  struct is_copy_constructible;
  ```
- !!!
#### `is_same` Struct
##### Introduction
- ```cpp
  template <class T, class U>
  struct is_same
  ```
- Inherits from [[#`integral_constant` Struct|integral_constant]]
- `value` is `true` if `T` and `U` are the same type. Otherwise `false`
#### `remove_cv` Struct
##### Introduction
- ```cpp
  template <class T>
  struct remove_cv
  ```
- CV as in `const` and `volatile`
- Struct removes those keywords
##### Attributes
- `type`
	- `T` without cv-qualifier
#### `remove_cvref` Struct
##### Introduction
- [[#`remove_cv` Struct|remove_cv]] and [[#`remove_reference` Struct|remove_reference]]
- ```cpp
  template <class T>
  struct remove_cvref;
  ```
##### Attributes
- `type`
	- Type referred to by `T` or `T` itself it is is not a reference, with `const` and `volatile` removed
#### `remove_reference` Struct
##### Introduction
- ```cpp
  template <class T>
  struct remove_reference;
  ```
- Removes reference from `T`
##### Members
- `type`
	- Type referred by `T` or `T` is it is not a reference
##### Types
- ```cpp
  templace <class T>
  using remove_reference_t = typename remove_reference<T>::type;
  ```
## `<unordered_map>` Header
- `std::unordered_map< <key_type>, <value_type>, <std::hash<K>> >`
	- A [[Hash Tables|hash table]]
### Methods
- `<hash_table>.at(<key>);`
	- Access the value at a key
- `<undordered_map>.contains(<key>);`
- `<hash_table>.insert({<key>, <value>});`
	- Inserts a key value pair into the table
- `auto [<iterator_name>, <boolean_name>] = <hash_table>.insert_or_assign(<key>, <value>);`
	-  You can check if it was insert and where it was inserted
	- Returns a `std::pair`
- `<hash_table>.find(<key>);`
	- Returns iterator that points at the element with the key
	- If the key does not exist, returns `.end()` iterator
- `<hash_table>.erase(<key_or_iterator>);`
	- Deletes the key with the element
	- You can also pass in an iterator
- `<unordered_map>.reserve(<int>);`
	- Allocates memory
## `<unordered_set>` Header
### Overview
- !!!
### Instantiation
- `std::unordered_set< <data_type> > <name> = {<values>};`
### Methods
- `<unordered_set>.clear()`
- `<unordered_set>.contains(<element>)`
- `<unordered_set>.empty()`
	- Returns true if empty
- `<unordered_set>.erase()`
	- `<unordered_set>.erase(<element>)`
	- `<unordered_set>.erase(<iterator>)`
- `<unordered_set>.find(<element>)`
	- Returns iterator pointing to element
- `<unordered_set>.insert(<element>)`
	- Adds element. If element already there, nothing happens
- `<unordered_set>.reserve(<int>);`
	- Allocates memory
- `<unordered_set>.size()`
## `<utility>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/utility)
### Introduction
- !!!
### Functions
- `declval`
	- ```cpp
	  template <class T>
	  std::add_rvalue_reference_t<T> declval() noexcept;
	  ```
	- !!!
- `forward`
	- Guess what it does? It forwards values in certain formats
	- ```cpp
	  template <class T>
	  constexpr T&& forward(std::remove_reference_t<T>& t) noexcept;
	  ```
		- Forwards lvalues as either lvalues or as rvalues, depending on T
			- Remember, perhaps forward can be used inside a wrapper. In such a case, maybe an argument is passed inside the wrapper as an lvalue or an rvalue, but either way, because we're passing the argument around, it will automatically decay into an lvalue. This is where forward comes around. We can pass the argument in under a type based on `T`. We can then deduce the appropriate type of `T`. If `T` is not a reference type, the argument will be forwarded as an rvalue. If `T` is a reference type, the argument will be forwarded as an lvalue
			- We can use the following example to think about it:
				- ```cpp
				  template <class T>
				  void wrapper(T&& arg) {
					  foo(std::forward<T>(arg));
				  }
				  ```
				- Where `foo()` is some other arbitrary function
				- We pass the value arg to `foo` accordingly now
	- ```cpp
	  template <class T>
	  constexpr T&& forward(std::remove_reference_t<T>&& t) noexcept;
	  ```
		- Forwards rvalues as rvalues and prohibits forwarding of rvalues as lvalues
- `in_place_index`
	- ```cpp
	  template <std::size_t T>
	  constexpr std::in_place_index_t<T> in_place_index();
	  ```
- `in_place_index_t`
	- ```cpp
	  template <std::size_t T>
	  struct in_place_index_t {explicit in_place_index_t() = default;};
	  ```
- `in_place_type`
	- ```cpp
	  template <class T>
	  constexpr std::in_place_type_t<T> in_place_type();
	  ```
- `in_place_type_t`
	- ```cpp
	  template <class T>
	  struct in_place_type_t {explicit in_place_type_t() = default;};
	  ```
- `move`
	- ```cpp
	  template <class T>
	  constexpr std::remove_reference_t<T>&& move(T&& t) noexcept;
	  ```
		- !!!
		- Moves contents from `<old_variable>` to `<new_variable>`
		- C++ will clean up the `<old_variable>`, it becomes empty
			- It lives on the stack but when it goes out of scope, the destructor will be called, and its heap memory will be used for something else
- `swap`
	- Exchanges given values
	- ```cpp
	  template <class T>
	  void swap(T& a, T& b);
	  ```
	- Swaps the values `a` and `b`
### Classes
#### `pair` Class
##### Introduction
- ```cpp
  template <class T1, class T2>
  struct pair;
  ```
- Provides a way to store two heterogenous objects as a single unit
- Specific case of `std::tuple` with two elements
## `<variant>` Header
### Sources
- [CPP Reference](https://en.cppreference.com/cpp/header/variant)
### Introduction
- !!!
### Classes
#### `variant` Class
##### Introduction
- ```cpp
  template <class ... Types>
  class variant;
  ```
- An instantiation of `variant` has a type of one of the listed types
##### Initialization
- ```cpp
  template <class T, class ... Args>
  constexpr explicit varirant(std::in_place_type_t<T>{}, Args&& ... args);
  ```
	- !!!
- ```cpp
  template <std::size_t I, class ... Args>
  constexpr explicit variant(std::in_place_index_t<T>{}, Args&& ... args);
  ```
	- !!!
##### Methods
- !!!
## `<vector>` Header
### Sources
- [CPPReference](https://en.cppreference.com/cpp/container/vector)
### Introduction
- !!!
### Classes
#### `vector` Class
##### Introduction
- ```cpp
  namespace pmr {
	  template<class T>
	  using vector = std::vector<T, std::pmr::polymorphic_allocator<T>>;
  }
  ```
	- Since C++17
##### Initialization
- `std::vector< <data_type(s)> > <name> = {<stuff>};`
- `std::vector< <data_types(s)> > <name>(<beginning>, <end>);
	- Used to initialize a vector from a part of a different vector
- `std::vector< <data_types(s)> > <name>(<amount_of_memory_you_want_to_preallocate>);
	- You can make a vector with a preallocate size this way
	- Can help prevent dynamic memory allocation when it is not needed
##### Methods
- `<vector>.back()`
	- Last element
- `<vector>.capacity()`
	- Returns max number of elements the vector can hold until it has to reallocate memory
- `<vector>.clear()`
	- Clears the entire array
- `const T* data() const`
	- Return a pointer to the first element of the vector
- `<vector>.empty()`
	- Checks whether the vector is empty
- `<vector>.erase(<iterator>)`
	- Removes element at a position
- `<vector>.front()`
	- First element
- `<vector>.insert(<iterator>, <element>)`
	- Adds an element at a position
- `<vector>.push_back(<element>);`
	- Adds an element to the end
- `<vector>.pop_back();`
	- Removes the last element
- `<vector>.reserve(<int>);`
	- Allocates memory
- `<vector>.size()`
	- Returns number of elements currently stored
# Binary Serialization
- !!!
# Command Line
## CLI11
- !!!
# Cryptography
## OpenSSL
- !!!
# Data Serialization
## JSON
### `nlohmann/json` Library
#### `<nlohmann/json.hpp>` Header
- !!!
## TOML
### `toml++` Library
#### `<toml++/toml.h>` Header
- !!!
## YAML
### `yaml-cpp` Library
#### `<yaml-cpp/yaml.h>` Header
- !!!
# Images
## `stb_image.h` Header
### Sources
- [GitHub - nothings  - stb - stb_image.h](https://github.com/nothings/stb/blob/master/stb_image.h)
- [Wikipedia - Channels](https://en.wikipedia.org/wiki/Channel_(digital_image))
### Installation
- !!!
### Introduction
- A C library to work with images
### Channels
- !!!
### Methods
- `void stbi_image_free(void* retval_from_stbi_load)`
	- Free the pointer holding the image
- `unsigned char* stbi_load(const char* filename, int* x, int* y, int* comp, int req_comp)`
	- `x`: Variable to hold width
	- `y`: Variable to hold height
	- `comp`: Variable to hold number of channels in file
	- `req`: Number of desired channels
	- Allocates space on the heap
## `std_image_resize2.h` Header
### Sources
- [GitHub - nothings  - stb - stb_image_resize2.h](https://github.com/nothings/stb/blob/master/stb_image_resize2.h)
### Installation
- !!!
### Introduction
- !!!
### Methods
- `unsigned char* stbir_resize_uint8_linear(const unsigned char* input_pixels, int input_w ,int input_h, int input_stride_in_bytes, unsigned char* output_pixels, int output_w, int output_h, int output_stride_in_bytes, stbir_pixel_layout pixel_layout)`
	- `input_pixel`: Pointer to the original image
	- `input_w`: Width of the original image in pixels
	- `input_h`: Height of the original image in pixels
	- `input_stride_in_bytes`: Width of the image in bytes
		- Recall a pixel can have multiple bytes, as there may be multiple channels
	- `output_pixels`: Pointer to the target image
	- `output_w`: Width of the output image in pixels
	- `output_h`: Height of the output image in pixels
	- `output_stride_in_bytes`: Width of the target image in pixels
	- `pixel_layout`: the image type. E.g. Grayscale, RGB. Use of the [[#`stbir_pixel_layout` Enum|stbir_pixel_layout]] enum is required
#### Enums
##### `stbir_pixel_layout` Enum
- Specifies
	- Number of channels
	- Order of channels
	- Whether colour is premultiplied by alpha
- `STBIR_1CHANNEL = 1`
- `STBIR_RGB = 3`
# Logging
## spdlog
- [[Projects (C++) (CPP)#Logging#spdlog|Here]]
# Machine Learning
## LibTorch
- !!!
# Mathematics
## Armadillo
- !!!
## Boost.Math
- !!!
## Boost.Multiprecision
- Install
	- On Mac
		- `brew install boost`
### `<boost/multiprecision/cpp_int.hpp>` Header
- Recommended to use an alias for the namespace
	- E.g. `namespace mp = boost::multiprecision;`
- `cpp_int`
	- It's actually a class
	- Generally recommended to 
		- Intialize as a string so that we can bypass the CPU's standard procedures which have limited capacity. If we use a string, it will get stored as text and Boost will convert the string and allocate memory for the number
		- Use curly brackets to intialize to directly call the constructor
	- E.g. `mp::cpp_int a{"1"};`
- `pow(<base>,<exp>)`
- `powm(<base>,<exp>,<mod>)`
	- For calculating large [[Congruences|congruences]]
	- [[Congruences#Fast Modular Exponentiation|Fast modular exponentiation]]
### `<boost/multiprecision/integer.hpp>` Header
- !!!
### `<boost/multiprecision/gmp.hpp>` Header
- GMP version
- Set up of GMP_C library
	- Installation
		- On Mac
			- `brew install gmp`
	- Linkage
		- On Mac
			- Alias
				- `alias gmpcompile++='clang++ -std=c++20 -I /opt/homebrew/include -L /opt/homebrew/lib -lgmp'`
			- Cmake
				- !!!
##### Tools
- `mpz_int`
	- E.g. `mpz_int a = 1;`
	- !!!
## Boost.Rational
### `<boost/rational.hpp>` Header
- !!!
## Eigen
### Sources
- [Brown University - CS224 - Eigen Tutorial](https://github.com/brown-cs-224/Eigen-Tutorial)
- [Eigen Documentation](https://libeigen.gitlab.io/eigen/docs-3.3/index.html)
	- [Eigen Documentation - Getting Started](https://libeigen.gitlab.io/eigen/docs-3.3/GettingStarted.html)
	- [Eigen Documentation - Quick Reference](https://libeigen.gitlab.io/eigen/docs-3.3/group__QuickRefPage.html)
		- [Eigen Documentation - Eigin/Core](https://libeigen.gitlab.io/eigen/docs-3.3/group__Core__Module.html)
			- [Eigen Documentation - MatrixBase](https://libeigen.gitlab.io/eigen/docs-3.3/classEigen_1_1MatrixBase.html)
				- [Eigen Documentation - inverse()](https://libeigen.gitlab.io/eigen/docs-3.3/classEigen_1_1MatrixBase.html#a7712eb69e8ea3c8f7b8da1c44dbdeebf)
			- [Eigen Documentation - Matrix](https://libeigen.gitlab.io/eigen/docs-3.3/classEigen_1_1Matrix.html)
			- [Eigen Documentation - Class Hierarchy](https://libeigen.gitlab.io/eigen/docs-3.3/TopicClassHierarchy.html)
	- [Eigen Documentation - Chapters](https://libeigen.gitlab.io/eigen/docs-3.3/topics.html)
		- [Eigen Documentation - Dense Matrix & Array Manipulation](https://libeigen.gitlab.io/eigen/docs-3.3/group__DenseMatrixManipulation__chapter.html)
			- [Eigen Documentation - Dot & Cross Product](https://libeigen.gitlab.io/eigen/docs-3.3/group__TutorialMatrixArithmetic.html#TutorialArithmeticDotAndCross)
			- [Eigen Documentation - Matrix & Vector Arithmetic](https://libeigen.gitlab.io/eigen/docs-5.0/group__TutorialMatrixArithmetic.html)
			- [Eigen Documentation - Array Operations](https://libeigen.gitlab.io/eigen/docs-3.3/group__TutorialArrayClass.html)
		- [Eigen Documentation - Dense Linear Problems & Decompositions](https://libeigen.gitlab.io/eigen/docs-3.3/group__DenseLinearSolvers__chapter.html)
		- [Eigen Documentation - Reductions, Visitors, & Broadcasting](https://libeigen.gitlab.io/eigen/docs-3.3/group__TutorialReductionsVisitorsBroadcasting.html)
	- [Eigen Documentation - Global Matrix Typedefs](https://libeigen.gitlab.io/eigen/docs-3.3/group__matrixtypedefs.html)
	- [Eigen Documentation - CMake](https://libeigen.gitlab.io/eigen/docs-5.0.1/TopicCMakeGuide.html)
- [YouTube - The Working Model - Machine Learning C++ Using Eigen Tutorial - Part 1 - ETL & Linear Regression](https://www.youtube.com/watch?v=jKtbNvCT8Dc)
- [Eigen Library Tutorial - Quick Reference](https://sites.cc.gatech.edu/classes/AY2015/cs4496_spring/Eigen.html)
- [Eigen for Statistical and Machine Learning Computing: A Lightweight C++ Tutorial with Python Bindings](https://arxiv.org/pdf/2605.22030)
- [YouTube - Aleksander Haber PhD - Intro to Eigen C++ Library](https://www.youtube.com/watch?v=XmtNr1TuO-E)
### Introduction
- A library for linear algebra
- Uses [[Core (C++) (CPP)#Curiously Recurring Template Pattern (CRTP)|CRTP]]
### Using it with CMake
- ```cmake
  # ...
  
  find_package (Eigen3 REQUIRED NO_MODULE)
  
  add_executable (example example.cpp)
  
  target_link_libraries (example Eigen3::Eigen)
  
  # ...
  ```
  - Header only, so you don't have to manage an actual `.a` or `.so` library file. But you still have to link it as a library
### `<Eigen/Core>` Header
#### Introduction
- The base module for Eigen
- Offers fundamental services
- Access to 
	- `Matrix` and `Array` classes
	- Basic linear algebra
	- Basic array manipulation
- Functions are encapsulated inside data types
- However, inverse and determinant functions are offered in the LU module, due to heavy computation optimizations relying on the [[Matrix Decompositions#LU Decomposition|LU matrix decomposition]]
#### Types
##### `Index` Type
- !!!
#### Classes
##### `Array<Scalar_, Rows_, Cols_, Options_, MaxROws_, MaxCols_>` Class
###### Introduction
- Inherits from [[#`ArrayBase<Derived>` Class|ArrayBase]]
###### Typedefs
- `ArrayNt`
	- `typedef Array<float, Dynamic, 1> ArrayXf`
- `ArrayNNt`
	- `typedef Array<double, Dynamic, Dynamic> ArrayXXd`
##### `ArrayBase<Derived>` Class
###### Introduction
- Inherits from [[#`DenseBase<Derived>` Class|DenseBase<Derived>]]
###### Methods
- `template <typename Derived> const AbsReturnType abs() const`
	- Returns an expression of the coefficient wise absolute value of `*this`
- `const ExpReturnType exp() const`
	- Returns an expression of the coefficient-wise exponential of `*this`
- `template <typename Derived> const LogReturnType log() const`
	- Returns an expression of the coefficient-wise natural logarithm of `*this`
- `MatrixWrapper<Derived> matrix()`
	- Returns a [[#`Matrix<_Scalar, _Rows, _Cols, _Options, _MaxRows, _MaxCols>` Class|Matrix]] representation of this array
- `template <typename Derived> const CwiseBinaryOp<internal::scalar_max_op<Scalar, Scalar>, const Derived, const CwiseNullaryOp<internal::scalar_constant_op<Scalar>, PlainObject>> max(const Scalar& other) const`
	- Returns an expression of the coefficient wise maximum of `*this` and the scalar `other`
- `template <typename Derived> const CwiseBinaryOp<internal::scalar_min_op<Scalar, Scalar>, const Derived, const CwiseNullaryOp<internal::scalar_constant_op<Scalar>, PlainObject>> min(const Scalar& other) const`
	- Returns an expression of the coefficient wise minimum of `*this` and the scalar `other`
##### `CwiseBinaryOp<BinaryOp, LhsType, RhsType>` Class
##### Introduction
- ```cpp
  template <typename BinaryOp, typename LhsType, typename Rhstype>
  class CwiseBinaryOp<BinaryOp, LhsType, RhsType>
  ```
	- `BinaryOp`: template functor implenting the operator
	- `LhsType`: type of the left hand side
	- `RhsType`: type of the right hand side
- Generic expression where a coefficient wise binary operator is applied to two expressions
##### `DenseCoeffsBase<Derived>` Class
- Inherits from [[#`EigenBase<Derived>` Class|EigenBase<Derived>]]
##### `DenseBase<Derived>` Class
###### Introduction
- Inherits from [[#`DenseCoeffsBase<Derived>` Class|DenseCoeffsBase<Derived>]]
- Base class for all dense
	- Matrices
	- Vectors
	- Arrays
	- And other dense objects
###### Methods
- `bool all() const`
	- Returns `true` if all coefficients are true
	- Example
		- ```cpp
		  Vector3f boxMin(Vector3f::Zero()), boxMax(Vector3f::Ones());
		  Vector3f p0 = Vector3f::Random(), p1 = Vector3f::Random().cwiseAbs();
		  // let's check if p0 and p1 are inside the axis aligned box defined by the corners boxMin,boxMax:

		  cout << "Is (" << p0.transpose() << ") inside the box: " << ((boxMin.array()<p0.array()).all() && (boxMax.array()>p0.array()).all()) << endl;
		  cout << "Is (" << p1.transpose() << ") inside the box: " << ((boxMin.array()<p1.array()).all() && (boxMax.array()>p1.array()).all()) << endl;
		  ```
- `bool any() const`
	- Returns true if at least one coefficient is true
- `CastXpr<NewType>::Type cast<NewType>() const`
	- `template<typename Derived>` and `template<typename NewType`
	- Return `*this` with the `Scalar` type casted to `NewType`
- `template <typename Derived> DenseBase<Derived>::ColwiseReturnType colwise()`
	- Returns a writeable [[#`VectorWiseOp<ExpressionType, Direction>` Class|VectorwiseOp]] wrapper of `*this` providing additional partial reduction operations
	- Allows operations to be broadcast against columns
- `template <typename Derived> template <typename OtherDerived> bool isApprox(const DenseBase<OtherDerived>& other, const RealScalar* prec = NumTraits<Scalar>::dummy_precision()) const`
	- Returns true if `*this` is approximately equal to `other`, within `prec`
	- Two vectors $\vec{v}$ and $\vec{w}$ are considered to be approximately equal within $p$ if $||\vec{v}-\vec{w}||\le p\min(||\vec{v}||,||\vec{w}||)$
	- For matrices, comparison is done using the Hilbert-Schmidt norm
	- Becuase the comparison is done multiplicatively, this function can be faulty when testing for matrices close to the zero matrices or vectors close to 0
- `internal::traits<Derived>::Scalar maxCoeff() const`
	- Return maximum of all coefficients in `*this`
- `template<typename Derived> internal::traits<Derived>::Scalar minCoeff() const`
	- Return the minimum of all coefficients in `*this`
- `static const DenseBase<Derived>::RandomReturnType Random()`
	- `template <typename Derived>`
	- Returns a fixed size random matrix
	- Numbers are uniformly spread through their whole definition range for integer types, and in the $[-1, 1]$ range for floating point scalar types
- `template <typename Derived> static const DenseBase<Derived>::RandomReturnType Random(Index rows, Index cols)`
	- Returns a dynamic size random matrix of size `rows` and `cols`
	- Numbers are uniformly spread through their whole definition range for integer types, and in the $[-1, 1]$ range for floating point scalar types
- `template <typename Derived> DenseBase<Derived>::RowwiseReturnType rowwise()`
	- Returns a writeable [[#`VectorWiseOp<ExpressionType, Direction>` Class|VectorwiseOp]] wrapper of `*this` providing additional partial reduction operations
	- Allows operations to be broadcast against rows
- `template <typename Derived> template <typename ThenDerived, typename ElseDerived> const Select<Derived, ThenDerived, ElseDerived> select(const DenseBase<ThenDerived>& thenMatrix, const DenseBase<ElseDerived>& elseMatrix) const`
	- Returns a matrix where each coefficient is equal to the respective coefficient in `thenMatrix` if the coefficient of `*this` is true, else the coefficient in `elseMatrix`
	- Example
		- Code:
			- ```cpp
			  #include <Eigen/Core>
			  
			  #include <iostream>
			  
			  int main(void) {
				  Eigen::MatrixXi matrix(3, 3) << 1, 2, 3, 4, 5, 6, 7, 8, 9;
				  matrix = (matrix.array() >= 5).select(-matrix, -matrix);
				  
				  std::cout << matrix << '\n';
				  
				  return 0;
			  }
			  ```
		- Output:
			- ```
			  1 2 3
			  4 -5 -6
			  -7 -8 -9
			  ```
- `template <typename Derived> template <typename ThenDerived, typename ElseDerived> const Select<Derived, ThenDerived, ElseDerived> select(const DenseBase<ThenDerived>& thenMatrix, const typename ThenDerived::Scalar& elseScalar) const`
	- Returns a matrix where each coefficient is equal to he respective coefficient in `thenMatrix` if the coefficient of `*this` is true, else `elseScalar` scalar
- `template <typename Derived> template <typename ThenDerived, typename ElseDerived> const Select<Derived, ThenDerived, ElseDerived> select(const typename ElseDerived::Scalar& thenScalar, const DenseBase<ElseDerived>& elseMatrix) const`
	- Returns a matrix where each coefficient is equal to the `thenScalar` scalar if the coefficient of `*this` is true, else the coefficient in `elseMatrix`
- `template <typename Derived> internal::traits<Derived>::Scalar sum() const`
	- Returns the sum of all coefficients of `*this`
- `Transpose<Derived> transpose()`
	- `template <typename Derived>`
	- Returns the transpose of `*this`
- `void transposeInPlace()`
	- In place version of `transpose()`
	- Replaces `*this` with its own transpose
- `static const DenseBase<Derived>::ConstantReturnType Zero()`
	- `template <typename Derived>`
	- Returns a fixed size zero matrix
- `static const DenseBase<Derived>::ConstantReturnType Zero(Index rows, Index cols)`
	- `template <typename Derived>`
	- Returns a dynamic size zero matrix
##### `CommaInitializer<XprType>` Class
###### Introduction
- ```cpp
  template<typename XprType>
  class CommaInitializer<XprType>;
  ```
###### Methods
- `XprType& finished()`
	- Returns the built matrix once all coefficients have been set
	- Calling `finished()` is optional
	- Meant to built expressions such as `quaternion.fromRotationMatrix((Matrix3f() << axis0, axis1, axis2).finished())`
##### `EigenBase<Derived>` Class
###### Introduction
- ```cpp
  template <typename Derived>
  class Eigen::EigenBase<Derived>
  ```
- The base class for all other classes in the Eigen library
- Represents the essence of a matrix
##### Methods
- `Eigen::Index cols() const`
	- Returns the number of columns
- `Derived& derived()` and `const Derived& derived() const`
	- A reference to the derived object
- `Eigen::Index rows() const`
	- Returns the number of rows
- `Eigen::Index size() const`
	- Returns the number of coefficients, or the size, in the matrix
##### `Inverse<Derived>` Class
- Inherits from [[#`InverseImpl<Derived>` Class|InverseImple<Derived>]]
##### `InverseImpl<Derived>` Class
- Inherits from either
	- [[#`MatrixBase<Derived>` Class|MatrixBase<Matrix>]]
	- Or [[#`ArrayBase<Derived>` Class|ArrayBase<Array>]]
##### `Map<PlainObjectType, MapOptions, StrideType>` Class
###### Introduction
- Inherits from [[#`MapBase<Derived, WriteAccessors>` Class|MapBase]]
- ```cpp
  template<typename PlainObjectType, int MapOptions, typename StrideType>
  class Eigen::Map<PlainObjectType, MapOptions, StrideType>
  ```
- `<PlainObjectType>`: the equivalent matrix type of the mapped data
- `<MapOptions>`: Specifies pointer alignment in bytes. `Unaligned` by default
- `<StrideType>`: Optionally specifies strides. By default, `Map` assumes the memory layout of a contiguous array
- Represents a matrix or vector expression that maps to an existing array of data
###### Initialization
- `Map<PlainObjectType, MapOptions, StrideType>(PointerArgType dataPtr, const StrideType& stride = StrideType())`
	- `dataPtr`: Pointer to the array to map
	- `stride`: Optional stride object
	- Fixed size case
- `Map<PlainObjectType, MapOptions, StrideType>(PointerArgType dataPtr, Index size, const StrideType& stride = StrideType())`
	- `dataPtr`: Pointer to the array to map
	- `size`: Size of the array
	- `stride`: Optional stride object
	- Dynamic size case
- `Map<PlainObjectType, MapOptions, StrideType>(PointerArgType dataPtr, Index rows, Index cols const StrideType& stride = StrideType())`
	- `dataPtr`: Pointer to the array to map
	- `stride`: Optional stride object
	- Dynamic size matrix case
###### Example
- ```cpp
  #include <iostream>
  
  #include <Eigen/Core>
  
  int main(void) {
	  int array[9];
	  
	  for (int i = 0; i < 9; ++i) {
		  array[i] = i;
	  }
	  
	  std::cout << Map<Matrix3i(array) << '\n';
  }
  ```
- ```cpp
  #include <Eigen/Core>
  
  Eigen::VectorXf create_output(unsigned char* input) {
	  return Eigen::Map<Eigen::Matrix<unsigned char, Eigen::Dynamic, 1>>(input, Global::SIZE);
  }
  ```
	- We can do this because of templating
##### `MapBase<Derived, WriteAccessors>` Class
###### Introduction
- Inherits from either
	- [[#`MatrixBase<Derived>` Class|MatrixBase<Derived>]]
	- Or [[#`ArrayBase<Derived>` Class|ArrayBase<Derived>]]
- ```cpp
  // !!!
  ```
##### `Matrix<_Scalar, _Rows, _Cols, _Options, _MaxRows, _MaxCols>` Class
###### Introduction
- ```cpp
  template <typename _Scalar, int _Rows, int _Cols, int _Options, int _MaxRows, int _MaxCols>
  class Eigen::Matrix<_Scalar, _Rows, _Cols, _Options, _MaxRows, _MaxCols>
  ```
- Inherits from [[#`PlainObjectBase<Derived>` Class|PlainObjectBase<Matrix>]]
- For matrices and vectors
	- Vectors are a special case of matrices; matrices with only one column
- The first three template parameters are required:
	- `_Scalar`: The number type for the coefficients
	- `_Rows`: The number of rows as an integer, or `Eigen::Dynamic`
	- `_Cols`: The number of columns as an `integer`, or `Eigen::Dynamic`
- The remaining three template parameters are optional:
	- !!!
###### Fixed vs Dynamic Size
- Dynamic sized matrix use a `Dynamic` type, indicating size is not known at compile time
	- For example, `typedef Matrix<int, Dynamic, Dynamic> MatrixXd` is a dynamic matrix that holds integers
- Fixed sized matrices should be used for smaller matrices, as Eigen holds values in an array for smaller matrices
	- As such, advantages present themselves, such as
		- The ability to avoid heap allocation
		- The ability for the compiler to perform loop unrolling
- Larger matrices should use dynamic sized arrays to avoid stack overflows
###### Dense vs Sparse Matrices
- !!!
###### Initialization
- `<matrix_type> A`
	- Allocates a matrix without using the heap and without initializing values
- `<matrix_type> A(<rows>, <cols>)`
	- Allocates a matrix of size `rows` by `cols`
- `<vector_type> A(<rows>)`
	- Allocates a vector with `rows` rows
- Comma initialization
	- We can initialize a matrix as such:
		- ```cpp
		  #include <Eigen/Core>
		  
		  int main(void) {
			  Eigen::Matrix3i A;
			  A << 1, 2, 3,
			       4, 5, 6,
			       7, 8, 9;
			       
			  return 0;
		  }
		  ```
- `<matrixtype> <name> = (<matrixtype>() << <values>).finished()`
	- An inline method of constructing a matrix with values
###### Working with a `Matrix`
- Value reassignment:
	- ```cpp
	  #include <iostream>
	  
	  #include <Eigen/Core>
	  
	  int main(void) {
		  Eigen::Matrix2i A;
		  A << 1, 2,
		       3, 4;
		  A(0, 0) = 2;
		  
		  std::cout << A << '\n';
		  
		  return 0;
	  }
	  ```
	- We can also take advantage of the `<<` operator, which is overloaded to modify values
		- ```cpp
		  #include <iostream>
	  
		  #include <Eigen/Core>
		  
		  int main(void) {
			  Eigen::Matrix2i A;
			  A << 1, 2,
			       3, 4;
			  A.rows(0) << 3, 3;
			  
			  std::cout << A << '\n';
			  
			  return 0;
		  }
		  ```
- Matrix multiplication
	- We use `*`, which is overloaded
		- ```cpp
		  #include <iostream>
	  
		  #include <Eigen/Core>
		
		  int main(void) {
			  Eigen::Matrix2i A;
			  A << 1, 2, 3, 4;
			  Eigen::Matrix2i B;
			  B << 2, 2, 3, 4;
			
			  std::cout << A * B << '\n';
			
			  return 0;
		}
		  ```
- Dot product between vectors
	- !!!
		- ```cpp
		  // !!!
		  ```
- Cross product between vectors
	- !!!
###### Methods
- !!!
###### Typedefs
- `MatrixNt` for `Matrix<t, N, N>`
	- `typedef Matrix<int, 2, 2> Matrix2i`
	- `typedef Matrix<int, 3, 3> Matrix2i`
	- `typedef Matrix<i, Dynamic, Dynamic> MatrixXi`
	- `typedef Matrix<double, 2, 2> Matrix2d`
	- `typedef Matrix<float, 2, 2> Matrix2f`
	- `typedef Matrix<std::complex<int>, 2, 2> Matrix2ci`
	- `typedef Matrix<std::complex<double>, 2, 2> Matrix2cd`
- `VectorNt` for `Matrix<t, N, 1>`
	- `typedef Matrix<int, 2, 1> Vector2i`
	- `typedef Matrix<int, 3, 1> Vector3i`
	- `typedef Matrix<i, Dynamic, 1> VectorXi`
	- `typedef Matrix<double, 2, 1> Vector2d`
	- `typedef Matrix<float, 2, 1> Vector2f`
	- `typedef Matrix<std::complex<int>, 2, 1> Vector2ci`
	- `typedef Matrix<std::complex<double>, 2, 1> Vector2cd`
- `RowVectorNt` for `Matrix<type, 1, N>`
	- `typedef Matrix<int, 1, 2> RowVector2i`
##### `MatrixBase<Derived>` Class
###### Introduction
- Inherits from [[#`DenseBase<Derived>` Class|DenseBase<Derived>]]
- Base class for all dense
	- Matrices
	- Vectors
	- And other related structures
###### Methods
- `ArrayWrapper<Derived> array()`
	- Returns an [[#`Array<Scalar_, Rows_, Cols_, Options_, MaxROws_, MaxCols_>` Class|Array]] representation of this matrix
- `void computeInverseAndDetWithCheck(ResultType& inverse, typename ResultType::Scalar& determinant determinant, bool& invertible, const RealScalar& absDeterminantThreshhold=NumTraits<Scalar>::dummy_precision()) const`
	- ```cpp
	  template <typename ResultType>
	  void computeInverseAndDetWithCheck(ResultType& inverse, typename ResultType::Scalar& determinant determinant, bool& invertible, const RealScalar& absDeterminantThreshhold=NumTraits<Scalar>::dummy_precision()) const
	  ```
	- Implementation is defined in the [[#`<Eigen/LU>` Header|LU]] module
	- `inverse`: Variable to store the inverse
	- `determinant`: Variable to store the deteriminant
	- `invertible`: Variable to store whether the matrix is invertible
	- `absDeterminantThreshhold`: Optional parameter controlling the invertibility check. The matrix will be declared invertible if the absolute value of its determinant is greater than this threshold
	- Computation of matrix inverse and determinant, with invertibility check
	- This is only for fixed-size square matrices of size up to 4x4
- `void computeInverseWithCheck(ResultType& inverse, bool& invertible, const RealScalar& absDeterminantThreshhold=NumTraits<Scalar>::dummy_precision()) const`
	- ```cpp
	  template <typename ResultType>
	  void computeInverseAndDetWithCheck(ResultType& inverse, bool& invertible, const RealScalar& absDeterminantThreshhold=NumTraits<Scalar>::dummy_precision()) const
	  ```
	- Implementation is defined in the [[#`<Eigen/LU>` Header|LU]] module
	- `inverse`: Variable to store the inverse
	- `invertible`: Variable to store whether the matrix is invertible
	- `absDeterminantThreshhold`: Optional parameter controlling the invertibility check. The matrix will be declared invertible if the absolute value of its determinant is greater than this threshold
	- Computation of matrix inverse and determinant, with invertibility check
	- This is only for fixed-size square matrices of size up to 4x4
- `MatrixBase<Derived>::PlainObject cross(const MatrixBase<OtherDerived& other) const)`
	- Defined in the [[#`<Eigen/Geometry>` Header|Geometry]] module
	- !!!
- `template <typename Derived> template <typename OtherDerived> const CwiseBinaryOp<internal::scalar_max_op<Scalar, Scalar>, const Derived, const OtherDerived> cwiseMax(const Eigen::MatrixBase<OtherDerived>& other) const`
	- Returns an expression of the coefficient wise max of `*this` and `other`
- `template <typename Derived> const CwiseBinaryOp <internal::scalar_max_op<Scalar, Scalar>, const Derived, const ConstantReturnType> cwiseMax(const Scalar& other) const`
	- Returns an expression of the coefficient wise max of `*this` and the scalar `other`
- `template <typename Derived> template <typename OtherDerived> const CwiseBinaryOp<internal::scalar_product_op<Derived::Scalar, OtherDerived::Scalar>, const Derived, const OtherDerived> cwiseProduct(const Eigen::MatrixBase<OtherDerived>& other) const`
	- Returns an expression of the Schur product, or the coefficient wise product, of `*this` and `other`
- `internal::traits<Derived>::Scalar determinant() const`
	- `template <typename Derived>`
	- Implementation is defined in the [[#`<Eigen/LU>` Header|LU]] module
	- Returns the determinant of `*this`
- `ScalarBinaryOpTraits<typename internal::traits<Derived::Scalar, typename internal::traits<OtherDerived>::Scalar>::ReturnType dot(const MatrixBase<OtherDerived& other) const`
	- `template<typename Derived>` and `tepmlate<typename OtherDerived>`
	- Only for vectors
	- Returns dot product of `*this` with `other`
- `const FullPivLU<typename MatrixBase<Derived>::PlainObject> fullPivLu const`
	- Defined in the [[#`<Eigen/LU>` Header|LU]] module
	- Returns the full pivoting LU decomposition of `*this`
- `static const MatrixBase<Derived>::IdentityReturnType Identity()`
	- `template <typename Derived>`
	- Returns `*this` as an identity matrix
	- Designed for fixed sized matrices
- `static const MatrixBase<Derived>::IdentityReturnType Identity(Index rows, Index cols)`
	- `template <typename Derived>`
	- Returns `*this` as an identity matrix with dimensions `rows` and `cols
	- Designed for dynamic sized matrices
- `const Inverse<Derived> inverse() const`
	- `template <typename Derived>`
	- Implementation is defined in the [[#`<Eigen/LU>` Header|LU]] module
	- Returns the inverse of `*this`
	- For small fixed sizes up to 4x4, this method uses cofactors. In the general case, this method uses the class
- `const PartialPivLU<typename MatrixBase<Derived>::PlainObject> lu() const`
	- `template <typename Derived>`
	- Defined in the [[#`<Eigen/LU>` Header|LU]] module
	- Returns the partial pivoting LU decomposition of `*this`
- `Derived& setIdentity()`
	- `template <typename Derived>`
	- Turn `*this` into an identity
##### `PlainObjectBase<Derived>` Class
###### Introduction
- Depending on whether or not `Matrix` or `Array` is used, the inherited type will be determined internally at compile time to be either [[#`MatrixBase<Derived>` Class|MatrixBase<Matrix>]] or [[#`ArrayBase<Derived>` Class|ArrayBase<Array>]], respectively
	- It uses `internal::dense_xpr_base<Derived>::type`
- This acts as a storage container base class for matrices and arrays in that it has state
###### Methods
- `Scalar* data()`
	- A pointer to the data array of this matrix
- `const Scalar* data() const`
	- A const pointer to the data array of this matrix
- `void resize(Index size)`
	- Resizes `*this`
	- Intended for dynamic vectors
- `void resize(Index rows, NoChange_t)`
	- Resizes the number of rows in `*this` but not the number of columns
	- Intended for dynamic size matrices
	- For `NoChange_t`, simply pass in `NoChange`
- `void resize(NoChange_t, Index columns)`
	- Resizes the number of columns in `*this` but not the number of rows
	- Intended for dynamic size matrices
	- For `NoChange_t`, simply pass in `NoChange`
- `void resize(Index rows, Index cols)`
	- Resizes `*this` such that it is `rows` by `cols`
	- Intended for dynamic size matrices
##### `Select<ConditionMatrixType, ThenMatrixType, ElseMatrixType>` Class
###### Introduction
- ```cpp
  template <typename ConditionMatrixType, typename ThenMatrixType, typename ElseMatrixType>
  class Select<ConditionMatrixType, ThenMatrixType, ElseMatrixType>;
  ```
	- `ConditionMatrixType`: type of the condition expression. Must be a boolean
	- `ThenMatrixType`: type of the then expression
	- `ElseMatrixType:` type of the else expression
- Inherits from either
	- [[#`MatrixBase<Derived>` Class|MatrixBase<Derived>]]
	- [[#`ArrayBase<Derived>` Class|ArrayBase<Derived>]]
- Expession of a coefficient wise version of the [[Core (C++) (CPP)#Ternary Operator|ternary operator]]
##### `Transpose<Derived>` Class
- Inherits from [[#`TransposeImpl<Derived>` Class|TransposeImpl<Derived>]]
#####  `TransposeImpl<Derived>` Class
- Inherits from either
	- [[#`MatrixBase<Derived>` Class|MatrixBase<Matrix>]]
	- Or [[#`ArrayBase<Derived>` Class|ArrayBase<Array>]]
##### `VectorwiseOp<ExpressionType, Direction>` Class
###### Introduction
- ```cpp
  template <typename ExpressionType, int Direction>
  class Eigen::VectorwiseOp<ExpressionType, Direction>
  ```
###### Methods
- !!!
#### Behaviours
##### Broadcasting
- !!!
### `<Eigen/Cholesky>` Header
- !!!
### `<Eigen/Dense>` Header
- Includes
	- [[#`<Eigen/Core>` Header|Core]]
	- [[#`<Eigen/Cholesky>` Header|Cholesky]]
	- [[#`<Eigen/Eigenvalues>` Header|Eigenvalues]]
	- [[#`<Eigen/Geometry>` Header|Geometry]]
	- [[#`<Eigen/LU>` Header|LU]]
	- [[#`<Eigen/QR>` Header|QR]]
	- And [[#`<Eigen/SVD>` Header|SVD]]
### `<Eigen/Eigen>` Header
- Includes Dense and Sparse headers; the entire Eigen library
### `<Eigen/Eigenvalues>` Header
- !!!
### `<Eigen/Geometry>` Header
#### Introduction
- Offers
	- Spatial transformations
	- And various geometric objects
#### Transformations
- !!!
#### Geometric Objects
- !!!
### `Eigen/Householder>` Header
- !!!
### `<Eigen/LU>` Header
#### Introduction
- Contains [[Matrix Decompositions#LU Decomposition !!!|LU]] decomposition stuff along with inversion and determinant support
#### Classes
##### `FullPivLU<_MatrixType>` Class
- !!!
##### `PartialPivLU<_MatrixType>` Class
###### Introduction
- !!!
###### Instantiation
- !!!
###### Methods
- `const Solve<PartialPivLU, Rhs> solve(const MatrixBase<Rhs>& b) const`
	- `template <typename Rhs>`
	- !!!
### `<Eigen/QR>` Header
- !!!
### `<Eigen/Sparse>` Header
#### Introduction
- Designed for matrices with mostly zeroes
#### Classes
- !!!
### `<Eigen/SVD>` Header
- !!!
## NTL
### `<NTL/ZZ.h>` Header
- !!!
### `<NTL/ZZ_pX.h>` Header
- !!!
# Networking
## Asio
- !!!
# Strings
## Boost.Algorithm.String
- `<boost/algorithm/string.hpp>`
