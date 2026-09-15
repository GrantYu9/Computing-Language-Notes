# Structure
## Introduction
- ```
  .
  |- bin
	  |- main
  |- build
	  |- ...
  |- lib
	  |- ...
  |- src
	  |- backend
		  |- CMakeLists.txt
		  |- ...
	  |- interface
		  |- CMakeLists.txt
		  |- main.cpp
	  |- CMakeLists.txt
  |- testing
	  |- CMakeLists.txt
	  |- ...
  |- CMakeLists.txt
  ```
## `include` Directory & Where to Place Header Files
- !!!
## `src` Directory
- !!!
## Sample Structure
- ```
  .
  |- bin
  |- build
  |- src
	  |- interface
	  |- backend
  |- tests
  ```
# Package Manager
## Conan
### Sources
- [Conan](https://conan.io/)
	- [Conan - Getting Started](https://docs.conan.io/2/tutorial/consuming_packages/build_simple_cmake_project.html)
### Installation
- !!!
### Introduction
- !!!
# Building
## CMake
- [[CMake|More]]
### Sources
- [CMake - Documentation](https://cmake.org/cmake/help/latest/index.html)
- [CMake - Guide](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
- [CMake - Tutorial](https://cmake.org/cmake/help/book/mastering-cmake/cmake/Help/guide/tutorial/index.html#)
- [Gregory Kelleher - Modern C++ Project Structuring](https://gregorykelleher.com/modern_cpp_project_structuring)
- [YouTube - PunchedTape - Introduction to CMake Crash Course](https://www.youtube.com/watch?v=7YcbaupsY8I&t)
- [StackOverflow - Difference between CMake Variables & Properties](https://stackoverflow.com/questions/49958208/what-is-the-difference-between-cmake-variables-and-properties)
- [Lei Mao - Interface, Public, & Private Visibilities in CMake](https://leimao.github.io/blog/CMake-Public-Private-Interface/)
- [StackOverflow - INCLUDE_DIRECTORIES versus INTERFACE_INCLUDE_DIRECTORIES](https://stackoverflow.com/questions/52059777/what-is-the-difference-between-include-directories-and-interface-include-directo)
### Introduction
- CMake is a language
- CMake is actually a build system generator, not a build tool or build system itself. It acts as a layer on top of traditional build tools like [[#GNU Make]], which quickly get messy in big projects
### Installation
#### Mac
- `brew install cmake`
### Basics
- At the bare minimum, to use CMake, we need to do 3 things:
	1. Indicate the minimum version of CMake needed
	2. Indicate the project name
	3. Tell CMake to create an executable from the project files
- For this example, assume a basic Hello World file:
	- ```cpp
	  #include <iostream>
	  
	  int main(void) {
		  std::cout << "Hello world!" << '\n';
		  
		  return 0;
	  }
	  ```
- In the following environment:
	- ```txt
	  .
	  |- hello_world.cpp
	  ```
- We now create a `CMakeLists.txt` file and specify the three requirements:
	- ```cmake
	  cmake_minimum_required(VERSION 4.3)
	  
	  project(my_project)
	  
	  add_executable(main hello_world.cpp)
	  ```
- Run `cmake -S .` to create the Makefile
- Run `make` to create the binary from the Makefile
- Run `./main` to run the binary
	- Expected output:
		- ```
		  Hello world!
		  
		  ```
### Recommended Courses of Action
#### Using a `build` Directory
- It is highly recommended to use a `build` directory so the files created by CMake can go into a singular, organized area
- We may have a directory that looks like this now:
	- ```
	  .
	  |- build
	  |- CMakeLists.txt
	  |- hello_world.cpp
	  ```
- We can then run `cmake -S . -B build` so the results of this command will go into `build`
- We then `cd` into `build` to run `make`
- And run `./main` to get the same expected output as in [[#CMake#Basics|above]]
#### Using a `bin` Directory
- We can make a directory in the project root called `bin` to place our binaries:
	- ```
	  .
	  |- bin
	  |- build
	  |- CMakeLists.txt
	  |- hello_world.cpp
	  ```
- Add the line `set(CMAKE_RUNTIME_OUTPUT_DIR ${CMAKE_SOURCE_DIR}/bin)` to our `CMakeLists.txt`:
	- ```cmake
	  cmake_minimum_required(VERSION 4.3)
	  
	  project(my_project)
	  
	  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
	  
	  add_executable(main hello_world.cpp)
	  ```
	- Place it before the `add_executable` command
	- We need to indicate the project root with `${CMAKE_SOURCE_DIR}` because `CMAKE_RUNTIME_OUTPUT_DIRECTORY` starts at the build path root first instead of the project root
- `cd` into `build` to run `cmake -S .. -B .` this time
- Run `make` while we are still in `build`
- And run `../bin/main` while we are still in `build`
#### Setting C++ Version & Extensions
- ```txt
  set(CMAKE_CXX_STANDARD 23) 
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  set(CMAKE_CXX_EXTENSIONS OFF)
  ```
- The first line enforces the standard
- The second line prevents attempted building using a previous version of C++
	- By default, CMake will attempt to use a previous version of C++ if the one in the enforced standard is not available. Hence, we enable this setting to force the usage of a minimum version of C++
- The third line enforces that only standard `c++` compiler extensions are allowed and not custom ones from compilers like GCC, Clang, or MSVC. This is to enforce portability
- We set this before `project()`
### Adding More Things
#### Setting a Compiler
- Setting a compiler should be done through the command line and not through the `CMakeLists.txt` file to avoid breaking cross-platform compatability
	- If you hard code the compiler to be `clang++`, someone on Linux or Windows will not be able to use your program
#### Combining Libraries
- !!!
#### Working with External Libraries
- Generally you will need to do 2 things:
	1. Locate the library with `find_package()`
	2. Attach it to the necessary targets with `target_link_libraries`
#### Working with Header Files
- We start with the following environment:
	- ```
	  .
	  |- bin
	  |- build
	  |- src
		  |- logic.cpp
		  |- logic.hpp
		  |- main.cpp
	  |- CMakeLists.txt
	  ```
- With the following files:
	- `logic.cpp`:
		- ```cpp
		  #include <string>
		  
		  std::string helloWorld() {
			  return "Hello world!"
		  }
		  ```
	- `logic.hpp`:
		- ```cpp
		  #pragma once
		  
		  #include <string>
		  
		  std::string helloWorld();
		  ```
	- `main.cpp`:
		- ```cpp
		  #include "logic.hpp"
		  
		  #include <iostream>
		  
		  int main(void) {
			  std::cout << helloWorld() << '\n';
			  
			  return 0;
		  }
		  ```
- Without using nested CMake files, we can use our top level CMake file as such:
	- ```cmake
	  cmake_minimum_required(VERSION 4.3)
	  
	  set(CMAKE_CXX_STANDARD 23) 
	  set(CMAKE_CXX_STANDARD_REQUIRED ON)
	  set(CMAKE_CXX_EXTENSIONS OFF)
	  
	  project(my_project)
	  
	  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
	  
	  add_library(logic src/logic.cpp)
	  
	  target_include_directories(logic PUBLIC src)
	  
	  add_executable(main src/main.cpp)
	  ```
- Look [[#CMake#Working with a Nested Environment|here]] to see how to resolve this issue with nested CMake files
#### Working with Header Only Libraries
- !!!
#### Working with Lots of Files
- Usually, you will have to specify them one by one
- It is poor practice to use a blanket `*` statement
#### Working with a Nested Environment
- Suppose the following environment:
	- ```
	  .
	  |- bin
	  |- build
	  |- src
		  |- backend
			  |- CMakeLists.txt
			  |- logic.cpp
			  |- logic.hpp
		  |- interface
			  |- CMakeLists.txt
			  |- main.cpp
		  |- CMakeLists.txt
	  |- CMakeLists.txt
	  ```
- With the following files:
	- `logic.hpp`:
		- ```cpp
		  #pragma once
		  
		  #include <string>
		  
		  std::string helloWorld();
		  ```
	- `logic.cpp`:
		- ```cpp
		  #include <string>
		  
		  std::string helloWorld() {
			  return "Hello world!";
		  }
		  ```
	- `main.cpp`:
		- ```cpp
		  #include "logic.hpp"
		  
		  #include <iostream>
		  
		  int main(void) {
			  std::cout << helloWorld() << '\n';
			  
			  return 0;
		  }
		  ```
- To use nested `CMakeList.txt` files to resolve linking, we plant a `CMakeLists.txt` file in each appropriate directory and each of them does a certain job:
	- `./CMakeLists.txt`
		- ```cmake
		  cmake_minimum_required(VERSION 4.3)

		  set(CMAKE_CXX_STANDARD 23)
		  set(CMAKE_CXX_STANDARD_REQUIRED ON)
		  set(CMAKE_CXX_EXTENSIONS OFF)
		
		  project(my_project)
		
		  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
		
		  add_subdirectory(src)
		  ```
		- This sets the global requirements and adds the `src` directory where the program is actually built
	- `./src/CMakeLists.txt`
		- ```cmake
		  add_subdirectory(backend)
		  add_subdirectory(interface)
		  ```
		- This simply just adds the two sub folders
	- `./src/backend/CMakeLists.txt`
		- ```cmake
		  add_library(backend logic.cpp)
		  
		  target_include_directories(backend PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
		  ```
		- This sets up the library for the logic that will be offered to the main program
	- `./src/interface/CMakeLists.txt
		- ```cmake
		  add_executable(main main.cpp)
		  
		  target_link_libraries(main backend)
		  ```
		- This creates the executable
		- Note that the library is visible becase we configured its visibility earlier
### Setting Things as Command Line Arguments
#### Compiler
- !!!
#### Debug Mode
- !!!
### Commands
- `cmake -B <location>`
- `cmake -S <location>`
- `cmake --version`
### Properties
- Properties are restricted within the scope of a target
- `CXX_EXTENSIONS`
	- Whether or not non standard compiler extensions outside of `c++` compiler are allowed
	- Enabled by default
- `CXX_STANDARD`
	- C++ minimum standard to build the target
- `CXX_STANDARD_REQUIRED`
	- Boolean for whether `CXX_STANDARD` is a requirement
	- If true, `CXX_STANDARD` must be used
	- Otherwise, the version of C++ may decay to something more available
	- Off by default
- `INCLUDE_DIRECTORIES`
	- Directories needed to create the target
- `INTERFACE_INCLUDE_DIRECTORIES`
	- Directories the target exposes as an interface
### Variables
- Variables are declared with the syntax: `${<variable_name>}`
- Using a variable that does not exist may not throw an error
- `CMAKE_ARCHIVE_OUTPUT_DIRECTORY`
	- Where archive target files are placed when built
- `CMAKE_BINARY_DIR`
	- Full path to the CMake build tree
	- Modifying this variable has undefined behaviour
- `CMAKE_BUILD_TYPE`
	- `Debug`: !!!
	- `Release`: !!!
- `CMAKE_CURRENT_SOURCE_DIR`
	- Full path to the current directory
	- Modifying this variable has undefined behaviour
- `CMAKE_CXX_EXTENSIONS`
	- Acts as a default value for `CXX_STANDARD_EXTENSIONS` upon creation of a target
- `CMAKE_CXX_STANDARD`
	- Acts as a default value for `CXX_STANDARD` upon creation of a target
- `CMAKE_CXX_STANDARD_REQUIRED`
	- Acts as a default value for `CXX_STANDARD_REQUIRED` upon creation of a target
- `CMAKE_LIBRARY_OUTPUT_DIRECTORY`
	- Where library target files are placed when built
- `CMAKE_PROJECT_NAME`
- `CMAKE_RUNTIME_OUTPUT_DIRECTORY`
	- Where `RUNTIME` target files will be built
- `CMAKE_SOURCE_DIR`
	- Full path to the project root
	- Modifying this variable has undefined behaviour
- `PROJECT_NAME`
	- !!!
### Functions
- Called "commands" in the documentation
- `add_executable(<name> <options>... <sources>...)`
	- Produces an executable from source files
	- `<name>`
		- Name of the produced executable
	- `<sources>`
		- As in source files
- `add_library(<name> INTERFACE)`
	- For header only libraries
- `add_library(<name> [STATIC | SHARED | MODULE] [EXCLUDE_FROM_ALL] <sources>...)`
	- Creates a library from source files
	- `STATIC`, `SHARED`, and `MODULE`
		- Specify the type of library to be created
		- [[Libraries#Types|Here]]
		- `MODULE`
			- !!!
		- `STATIC` by default
- `add_subdirectory(source_dir [binary_dir] [EXCLUDE_FROM_ALL] [SYSTEM])`
	- Adds a subdirectory to the build
- `add_test(NAME <name> COMMAND <command> [<arg>...][CONFIGURATIONS <config>...] [WORKING_DIRECTORY <dir>] [COMMAND_EXPAND_LISTS] [BUILD_DEPENDS <dependencies>...])`
	- Adds a test named `<name>`
	- Only generates tests if `enabled_testing()` has been invoked
- `cmake_minimum_required(VERSION <min>[...<policy_max>] [FATAL_ERROR])`
	- Establishes a minimum CMake version for a project
	- `<min>`
		- The minimum version number
- `enable_testing()`
	- Enables testing for the current directory and below
- `find_package(<PackageName> [<version>] [REQUIRED] [COMPONENTS <components>...])`
	- Find a package and load package-specific details
- `include(<file|module> [OPTIONAL] [RESULT_VARIABLE <var>] [NO_POLICY_SCOPE] [NO_DIAGNOSTIC_SCOPE])`
	- Loads and runs CMake code from the file given
	- It runs scripts
- `option()`
	- !!!
- `project(<PROJECT-NAME> [<language-name>...])` or `project(<PROJECT-NAME> [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]] [COMPAT_VERSION <major>[.<minor>[.<patch>[.<tweak>]]]] [SPDX_LICENSE <license-string>] [DESCRIPTION <description-string>] [HOMEPAGE_URL <url-string>] [LANGUAGES <language-name>...])`
	- Sets the name of the project and stores it under the variable `PROJECT_NAME`
	- When called from the top level `CMakeLists.txt` file, it also stores the project name under the variable `CMAKE_PROJECT_NAME`
	- Also sets the variables:
		- !!!
- `set(<variable> <value>... [PARENT_SCOPE])`
	- Set or unset `<variable>`
	- If `<value>` is not specified, this will behave just like `unset(<variable>)`
- `set_directory_properties()`
	- !!!
- `set_property()`
	- !!!
- `target_include_directories(<target> [SYSTEM] [AFTER | BEFORE] {INTERFACE | PUBLIC | PRIVATE} <dir...[{INTERFACE|PUBLIC|PRIVATE} <dir>...]...)`
	- Includes directories for a target for compilation and to offer in its interface
	- `INTERFACE`, `PUBLIC`, and `PRIVATE`
		- They specify the scope of the subseqent directories
		- `PRIVATE`
			- Directories will be listed under the `INCLUDE_DIRECTORIES` property
		- `INTERFACE`
			- Directories will be listed under the `INTERFACE_INCLUDE_DIRECTORIES` property
		- `PUBLIC`
			- Directories will be listed under both the `INCLUDE_DIRECTORIES` and `INTERFACE_INCLUDE_DIRECTORIES` properties
- `target_link_libraries(<target> [INTERFACE | PUBLIC | PRIVATE] <item>... ...)`
	- Links a library to a target
	- `<item>` can be
		- A library target name
			- Created from `add_library()`
		- A full path to a library file
- `unset(<variable> [PARENT_SCOPE])`
	- Removes a normal variable from the current scope, causing it to become undefined
### Build System
#### Archive Files
- !!!
#### Library Files
- !!!
#### Runtime Files
- !!!
### `.cmake` Files & Scripting
- !!!
## GNU Make
### Sources
- !!!
### Introduction
- !!!
### Command Line
- `make`
	- !!!
# Documentation Tools
## Doxygen
### Sources
- [Doyxgen - Manual](https://www.doxygen.nl/manual/)
	- [Doxygen - Tutorial](https://www.doxygen.nl/manual/starting.html)
	- [Doxygen - Special Commands](https://www.doxygen.nl/manual/commands.html)
	- [Doxygen - Command Line](https://www.doxygen.nl/manual/doxygen_usage.html)
	- [Doxygen - Configuation](https://www.doxygen.nl/manual/config.html)
	- [Doxygen - Usage](https://www.doxygen.nl/manual/doxygen_usage.html)
- [Geeks for Geeks - Doxygen](https://www.geeksforgeeks.org/cpp/doxygen-cpp-documentation/)
- [Wikipedia](https://en.wikipedia.org/wiki/Doxygen)
- [StackOverflow - Document Header Files or Source Files](https://softwareengineering.stackexchange.com/questions/84071/is-it-better-to-document-functions-in-the-header-file-or-the-source-file)
### Introduction
- A documentation generator
- Reads specially formatted comments in source code and outputs it in certain formats
- Requires a configuation file
### Configuation
#### Introduction
- You set options
- Format:
	- `<OPTION> = <value> ...`
		- Where `<OPTION>` must be in screaming snake case
	- Or `<OPTION> += <value> ...` to append values to a list if `<OPTION>` can take lists
	- To add multiple values, separate them with a space
- You can use `#` to establish comments, like in CMake or Python
- For file paths, you can list them as is like `./src` or `./src/backend/main.cpp`
#### Modularity
- You can include another config file as such:
	- `@INCLUDE = <other_config_file_name>`
- Searching is done in the current directory. To specify another directory, use `@INCLUDE_PATH`:
	- `@INCLUDE_PATH = <config_file_dir>`
#### Options
- `EXTRACT_ALL = <bool>`
	- If yes, will assume all entities are documented
	- Private and static members will be hidden unless `EXTRACT_PRIVATE` and `EXTRACT_STATIC` tags, respectively, are set to yes
	- By default, no
- `EXTRACT_PRIVATE = <bool>`
	- If yes, private members will also be documented
	- By default, no
- `EXTRACT_STATIC = <bool>`
	- If yes, static members will also be documented
	- By default, no
- `EXCLUDE`
	- Exclude files or directories
- `EXCLUDE_PATTERNS`
	- Use patterns to exclude files or directories
- `GENERATE_LATEX = <bool>`
	- Whether or not a `latex` folder will be generated
	- By default, yes
- `INPUT = <path> ...`
	- Specifies where to begin search
	- By default, where `doxygen` is ran
- `HAVE_DOT = <bool>`
	- If yes, Doxygen will assume `dot` is available
	- By default, no
- `OUTPUT_DIRECTORY`
- `PROJECT_NAME`
- `RECURSIVE = <bool>`
	- Whether or not to recursively search given `INPUT`
	- Off by default
#### Example
- ```txt
  INPUT = ../src
  RECURSIVE = ON
  OUTPUT_DIRECTORY = .
  PROJECT_NAME = my_project
  ```
### Documenting
- Document header files, not source code
#### Special Comment Blocks
- ```cpp
  /** <brief>
   * <text>
   */
  ```
- ```cpp
  /// <brief>
  /// <text>
  ///
  ```
- Always written above what you want to document
#### Special Comment Lines
- `/** <comment> */
- `int var; ///< <description>`
#### Special Commands
- Start with either `\` or `@`
- Argument range
	- `<>` braces
		- Argument is a single word
	- Parenthesis
		- Argument extends until end of line on which command was found
	- Braces
		- Argument extends until next paragaph
			- Paragraphs are determined by a blank line or a section indicator
- `@brief {description}`
- `@cite['{'[option]'}'] <label>`
- `@deprecated {description}`
- `@details {desciption}`
- `@file [<file_name>]`
	- Required for global functions
- `@invariant {description}`
- `@param[[<direc>]] <param_name> {description}`
	- `[<direc>]` is the direction of the parameter
		- See [[Class Diagram#Operations|this]] for a further explanation of parameter direction
		- E.g. `[in]`, `[out]`, `[in, out]`
- `@note {text}`
- `@ref <name> ["(text)"]`
	- Creates a hyperlink to `<name>`
- `@returns {description}`
- `@see {references}`
- `@throw <exception_object_name> {description}`
- `@warning {message}`
#### Automatic Documentation
- !!!
#### Cases
##### Global Functions
- Files that contain a global function must have the `@file` special command
#### Style
- [[Style (C++) (CPP)|Here]]
- Just use [[Style (Python)|Python]] style at this point 🥀🥀🥀
### Generating Documentation
- Run `doxygen <config_file>`
- Open `html/index.html` to see the documentation
### Command Line
- `doxygen <config_file>`
	- Generates output of documentation
- `doxygen [-s] -g [<name>]`
	- Creates a configuration file of `<name>`
	- By default, creates a configuation file named `Doxyfile`
	- With `-s`, removes comments
- `doxygen --help`
- `doxygen --version`
### Examples
#### Functions
- Suppose the following system:
	- ```
	  .
	  |- docs
		  |- doxyfile
	  |- src
		  |- backend
			  |- logic.cpp
			  |- logic.hpp
		  |- interface
			  |- main.cpp
	  ```
- `logic.hpp`:
	- ```cpp
	  #pragma once
	  
	  /** @file logic.hpp
	   * @brief Provides basic operations
	   */
	
	  /** @brief Adds x and y and returns the sum
	   *
	   * @param x The augend
	   * @param y The addend
	   *
	   * @returns x The sum
	   */
	  int add(const int x, const int y);
	  
	  /** @brief Adds x and y and returns the sum
	   *
	   * @param x The minuend
	   * @param y The subtrahend
	   *
	   * @returns x The difference
	   */
	  int subtract(const int x, const int y);
	  ```
- `doxyfile`:
	- ```
	  GENERATE_LATEX = NO
	  INPUT = ../src/backend
	  OUTPUT_DIRECTORY = .
	  PROJECT_NAME = my_project
	  ```
#### Classes
- Suppose the following system:
	- ```
	  .
	  |- docs
		  |- doxyfile
	  |- src
		  |- backend
			  |- logic.cpp
			  |- logic.hpp
		  |- interface
			  |- main.cpp
	  ```
- `logic.hpp`:
	- ```cpp
	  #pragma once
	  
	  /** @file logic.hpp
	   * @brief Provides basic operations
	   */
	
	  /** @brief An interface that stores two numbers and supports basic operations 
	   * between them 
	   */
	  class Calculator {
	  private:
		  const int x; ///< An integer
		  const int y; ///< Another integer
	  
	  public:
		  /** @brief Sets up the calculator
		   * 
		   * @param x For @ref x
		   * @param y For @ref y
		   */
		  Calculator(const int x, const int y) : x(x), y(y) {}
		  
		  /** @brief Adds @ref x and @ref y and returns the sum
		   *
		   * @returns The sum
		   */
		  int add() const;
		  
		  /** @brief Subtracts @ref x and @ref y and returns the difference
		   *
		   * @returns The difference
		   */
		  int subtract() const;
	  };
	  ```
- `doxyfile`:
	- ```
	  GENERATE_LATEX = NO
	  EXTRACT_PRIVATE = YES
	  INPUT = ../src/backend
	  OUTPUT_DIRECTORY = .
	  PROJECT_NAME = my_project
	  ```
# Debugging
## GDB (GNU Debugger)
### Sources
- [Geeks for Geeks](https://www.geeksforgeeks.org/c/gdb-step-by-step-introduction/)
### Introduction
- !!!
## LLDB (Low Level Debugger)
### Sources
- [National Institute of Standards & Technology - Introduction to LLVM LLDB](https://math.nist.gov/oommf/doc/progman20b0/progman/Introduction_to_LLVM_lldb.html)
- [LLVM - LLDB Documentation](https://lldb.llvm.org/)
	- [LLVM - LLDB Tutorial](https://lldb.llvm.org/use/tutorial.html)
- [RedHat - LLDB Tutorial](https://docs.redhat.com/en/documentation/red_hat_developer_tools/1/html/using_llvm_13.0.1_toolset/assembly_the-lldb-debugger)
- [YouTube - Mike Shah - Learn the LLDB Basics in 11 Minutes](https://www.youtube.com/watch?v=v_C1cvo1biI)
### Installation
#### Mac
- Comes with XCode
- `xcode-select --install`
### Introduction
- A debugger
### Breakpoints
- Set breakpoints with `b` or `breakpoint set`
### Running a Program with Debugger
- Compile the program correctly
	- Look [[Command Line (C++) (CPP)#`clang++` Command|here]] to see what's up
- Run `lldb <binary` to enter the environment
- Set breakpoints and run `(lldb) run` to initiate debugging
### Commands
- `(lldb) breakpoint`
	- `(lldb) breakpoint delete [<breakpoint_id> | <breakpoint_id_list>]`
		- Deletes a breakpoint given a breakpoint ID
		- If nothing is specified, deletes all breakpoints
	- `(lldb) breakpoint list`
	- `(lldb) {b | breakpoint set}`
		- `(lldb) b <function>`
		- `(lldb) b {-N | --breakpoint-name} <name>`
			- Add to the list of names for a breakpoint
		- `(lldb) b {-O | --exception-typename} <name>`
			- Breakpoint will only stop if an exception is thrown of type `<name>` is thrown
		- `(lldb) b {-a | --address} <address>`
		- `(lldb) b {-l | --line} <line> [{-f | --file} <file>]` or `(lldb) b <file>:<line>`
		- `(lldb) b {-i | --ignore-count} <count>`
			- Number of times to ignore a breakpoint before stopping
- `(lldb) down`
	- !!!
- `(lldb) {e | exit | q | quit}`
- `(lldb) frame`
	- `(lldb) {f | frame select} [<frame_index>]`
		- Select a stack frame
		- By default, selects current stack frame, which is 0 by default
- `(lldb) help`
	- Displays information about all commands
	- `(lldb) help <command>`
		- Displays further information about a command
- `(lldb) {j | jump} {<line> | *<address>}`
	- Modify the program counter
- `(lldb) {l | list}`
	- List subsequent lines of code. Starts at the top of the current file
	- `(lldb) l <address>`
	- `(lldb) l <file>:<line>`
	- `(lldb) l <function`
	- `(lldb) l <line>`
- `(lldb) memory`
	- `(lldb) memory find {-e <expression> | -s <string>} [-c <count>] [-o <offset>] <address_start> <address_end>`
		- Find a pattern from within the start address to the end address
		- `<count>`: how many times to perform the search
	- `(lldb) {x | memory read} <address>`
		- Display value at an address
- `(lldb) {n | next}`
	- Step over
	- `(lldb) n -c <count>`
		- How many times to step over
- `(lldb) {p | print} <variable>`
	- Print the information of a variable
	- You can run `(lldb) p &<variable>` to get the address
- `(lldb) process`
	- `(lldb) {c | continue | process continue}`
	- `(lldb) {kil | kill | process kill}`
		- Kill the current process
- `(lldb) {r | run} [<argument> ...]`
	- Run the program, optionally with arguments
- `(lldb) {s | step}`
	- Step into
	- `(lldb) s -c <number>`
		- Number of  lines you wish to step
	- `(lldb) s -e <line>`
		- Line number  you wish to stop stepping at
- `(lldb) source`
	- `(lldb) source info`
		- Gives info about current process
- `(lldb) thread`
	- `(lldb) {bt | thread backtrace} [-c <count>] [-e <boolean>] [<thread-index> [<thread-index> [...]]]`
		- Show backtraces of thread call stacks.  Defaults to the current thread, thread indexes can be specified as arguments
		- Use thread index `all` to see all threads
		- Use thread index `unique` to see threads grouped by unique call stacks
		- `-c <count>`: number of frames
			- `0` for all
		- `-e <boolean>`: show extended backtrace
- `(lldb) up`
	- !!!
- `(lldb) {v | var | vo}`
	- Show variables for current stack frame
- `lldb <binary_file>`
	- Enter a binary with LLDB
- `lldb --version` or `(lldb) version`
	- Version of debugger
## VSCode
- !!!
# Testing
## GoogleMock
- !!!
## GoogleTest
### Sources
- [GoogleTest - CMake](https://google.github.io/googletest/quickstart-cmake.html)
- [GoogleTest - Guide](https://google.github.io/googletest/)
	- [GoogleTest - Primer](https://google.github.io/googletest/primer.html)
	- [GoogleTest - Parametrization](https://google.github.io/googletest/advanced.html#how-to-write-value-parameterized-tests)
	- [GoogleTest - Friend Test](https://en.wikipedia.org/wiki/Backpropagation)
- [Geeks for Geeks](https://www.geeksforgeeks.org/software-testing/gtest-framework/)
- [StackOverflow - Assert or Expect](https://stackoverflow.com/questions/2565299/using-assert-and-expect-in-googletest)
### Installation
#### Mac
- !!!
### Introduction
- `<gtest/gtest.h>`
- General structure for a test
	- ```c++
	  TEST(<suite_name>, <test_name>) {
		  // Expects & asserts
	  }
	  ```
- We can run all tests or tests of a suite name
### Using it with CMake
- Another `CMakeLists.txt` file will be needed in the `testing` folder
- We create an executable from the test file and configure the `CMakeLists.txt` as such:
	- ```cmake
	  enable_testing()
	  
	  find_package(GTest REQUIRED)
	  
	  add_executable(<executable_name> <test_file_names>)
	  
	  target_link_libraries(<executable_name> GTest::gtest_main
		  <other_depedencies>
	  )
	  
	  include(GoogleTest)
	  
	  gtest_discover_tests(<executable_name>)
	  ```
### Asserts
- Fatal error; will stop tests
- `ASSERT_EQ(<value1>, <value2>)`
- `ASSERT_FALSE(<condition>)`
- `ASSERT_NE(<val_1>, <val_2>)`
- `ASSERT_STREQ(<string1>, <string2>)`
- `ASSERT_TRUE(<condition>)`
- `ASSERT_THROW(<statement>, <throw_type>)`
### Expects
- Non-fatal error; will not stop tests
- `EXPECT_EQ(<value1>, <value2>)`
- `EXPECT_FALSE(<condition>)`
- `EXPECT_LT(<value>, <value2>)`
- `EXPECT_NE(<val_1>, <val_2>)`
- `EXPECT_NEAR(<val_1>, <val_2>, <abs_error>)`
- `EXPECT_NO_THROW(<statement>)`
- `EXPECT_STREQ(<string1>, <string2>)`
- `EXPECT_TRUE(<condition>)`
- `EXPECT_THROW(<statement>, <throw_type>)`
### Running Tests
#### Out of the Box
- We need to modify our `main` function:
	- ```cpp
	  #include <gtest/gtest.h>
	  
	  int main(int argc, char** argv) {
		  // !!!
	  }
	  ```
#### With CMake
- If you followed the [[#GoogleTest#Using it with CMake|configuration steps]] correctly, we simply have to run the executable in our `bin` folder
### Fixtures
- We use fixtures to assist in running tests that use the same data
- We create a test class representing the fixture object we wish to pass. It must extend `::testing::Test`:
	- ```cpp
	  #include "logic.hpp"
	  
	  #include <gtest/gtest.h>
	  
	  class TestFixturePair : public ::testing::Test {
	  protected:
		  int x;
		  int y;
		  
		  void SetUp() override {
			  x = 1;
			  y = 2;
		  }
	  };
	  ```
	- We can either put the set up in a constructor or the set up. Both are also optional
	- Furthermore, we may optionally override the `TearDown()` method
- And we create tests with the `TEST_F` macro, not the `TEST` macro. Furthermore, we pass the name of the fixture class we wish to pass as the first arguement:
	- ```cpp
	  #include "logic.hpp"
	  
	  #include <gtest/gtest.h>
	  
	  class TestFixturePair : public testing::Test {
	  protected:
		  int x;
		  int y;
		  
		  void SetUp() override {
			  x = 1;
			  y = 2;
		  }
	  };
	  
	  TEST_F(TestFixturePair, TestAdd) {
		  EXPECT_EQ(add(x, y), 3);
	  }
	  
	  TEST_F(TestFixturePair, TestSubtract) {
		  EXPECT_EQ(subtract(y, x), 1);
	  }
	  ```
### Parametrization
- We need a test class that implements `testing::WithParamInterface<T>`, where `T` is the type of parameter we'll pass. If you want to pass multiple parameters, use a container to hold the types of the parameters you wish to pass, and unpack it later. It will act as a fixture:
	- ```cpp
	  #include "logic.hpp"
	  
	  #include <gtest/gtest.h>
	  
	  #include <tuple>
	  
	  class TestLogicParametrized : public testing::TestWithParam<std::tuple<int, int>> {};
	  ```
- Use the `TEST_P` macro to write a generalized version of the tests you wish to use, passing in the test class above as if it were a fixture:
	- ```cpp
	  #include "logic.hpp"
	  
	  #include <gtest/gtest.h>
	  
	  #include <tuple>
	  
	  class TestLogicParametrized : public testing::TestWithParam<std::tuple<int, int>> {};
	  
	  TEST_P(TestLogicParametrized, TestAdd) {
		  auto [x, y] = GetParam();
		  
		  EXPECT_EQ(add(x, y), x + y);
	  }
	  ```
	- As you can see, we unpack it with `auto` and `GetParam()`
	- We write the generalized assert statement under our unpacking statement
	- Notice we use braces
- Finally, we inject our parametrized test cases with the `INSTANTIATE_TEST_SUITE_P` macro:
	- ```cpp
	  #include "logic.hpp"
	  
	  #include <gtest/gtest.h>
	  
	  #include <tuple>
	  
	  class TestLogicParametrized : public testing::TestWithParam<std::tuple<int, int>> {};
	  
	  TEST_P(TestLogicParametrized, TestAdd) {
		  auto [x, y] = GetParam();
		  
		  EXPECT_EQ(add(x, y), x + y);
	  }
	  
	  INSTANTIATE_TEST_SUITE_P(TestsAdd, TestLogicParametrized,
		  testing::Values(
			  std::tuple{1, 2}, 
			  std::tuple{2, 3}
		  );
	  );
	  ```
	- We create a name for the parametrized test suite, and pass in the parametrized fixture as the second argument, with `testing::Values()` and our values as our third argument
- A more comprehensive example:
	- ```cpp
	  #include "logic.hpp"

	  #include <gtest/gtest.h>
	  
	  #include <tuple>
	  
	  class TestLogicParametrizedAdd : public testing::TestWithParam<std::tuple<int, int>> {};
	  class TestLogicParametrizedSubtract : public testing::TestWithParam<std::tuple<int, int>> {};
	
	  TEST_P(TestLogicParametrizedAdd, TestAdd) {
	      auto [x, y] = GetParam();
	    
	      EXPECT_EQ(add(x, y), x + y);
	  }
	
	  TEST_P(TestLogicParametrizedSubtract, TestSubtract) {
	      auto [x, y] = GetParam();
	    
	      EXPECT_EQ(subtract(x, y), x - y);
	  }
	
	  INSTANTIATE_TEST_SUITE_P(TestsAdd, TestLogicParametrizedAdd,
	      testing::Values(
	          std::tuple{1, 2}, 
	          std::tuple{2, 3}
	      )
	  );
	
	  INSTANTIATE_TEST_SUITE_P(TestsSubtract, TestLogicParametrizedSubtract,
	      testing::Values(
	          std::tuple{1, 2}, 
	          std::tuple{2, 3}
	      )
	  );
	  ```
	- Note in this example, we need to be careful with the name of the parametrized fixture we craete and what we pass in
### Example
- Suppose the following system:
	- ```
	  |- bin
	  |- build
	  |- src
		  |- backend
			  |- CMakeLists.txt
			  |- logic.cpp
			  |- logic.hpp
		  |- interface
			  |- CMakeLists.txt
			  |- main.cpp
	  |- tests
		  |- CMakeLists.txt
		  |- test_logic.cpp
	  |- CMakeLists.txt
	  ```
- With the following files:
	- `logic.cpp`:
		- ```cpp
		  int add(const int x, const int y) {
			  return x + y;
		  }
		  
		  int subtract(const int x, const int y) {
			  return x - y;
		  }
		  ```
	- `logic.hpp`:
		- ```cpp
		  #pragma once
		  
		  int add(const int x, const int y);
		  
		  int subtract(const int x, const int y);
		  ```
	- `test_logic.cpp`:
		- ```cpp
		  #include "logic.hpp"
		  
		  #include <gtest/gtest.h>
		  
		  TEST(TestLogic, TestAdd) {
			  EXPECT_EQ(add(1, 2), 3);
		  }
		  
		  TEST(TestLogic, TestAdd) {
			  EXPECT_EQ(subtract(2, 1), 1);
		  }
		  ```
	- `./CMakeLists.txt`:
		- ```cmake
		  cmake_minimum_required(VERSION 4.3)

		  set(CMAKE_CXX_STANDARD 23)
		  set(CMAKE_CXX_REQUIRED ON)
		  set(CMAKE_CXX_EXTENSIONS OFF)
		
		  project(my_project)
		
		  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
		
		  add_subdirectory(src)
		  add_subdirectory(tests)
		  ```
	- `./tests/CMakeLists.txt`:
		- ```cmake
		  cmake_minimum_required(VERSION 4.3)

		  set(CMAKE_CXX_STANDARD 23)
		  set(CMAKE_CXX_REQUIRED ON)
		  set(CMAKE_CXX_EXTENSIONS OFF)
		
		  project(my_project)
		
		  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
		
		  add_subdirectory(src)
		  add_subdirectory(tests)
		  ```
	- `./src/CMakeLists.txt`:
		- ```cmake
		  add_subdirectory(backend)
		  add_subdirectory(interface)
		  ```
	- `./src/backend/CMakeLists.txt`:
		- ```cmake
		  add_library(backend logic.cpp)

		  target_include_directories(backend PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
		  ```
- Inside `./build`:
	- We run `cmake -S .. -B .`
	- We run `make`
	- We run `../bin/tests`
	- It should be observable that tests pass
### Command Line
- `<binary> --gtest_break_on_failure`
	- !!!
# Logging
## spdlog
- Install
	- Mac
		- `brew install spdlog`
- `<spdlog/spdlog.h>`
### Log Levels
- There are 7 log levels, each of a different sevurity
- Upon setting a level, only messages of that level or higher will be recorded
#### Levels
- Highest to lowest severity
- `off`
	- Silences the logger
- `critical`
	- `spdlog::critical()`
	- Total disaster
	- E.g. Out of memory
- `error`
	- `spdlog::error()`
	- Feature failed
	- E.g. Could not save file
- `warn`
	- `spdlog::warn()`
	- Something is off, but the program is generally okay
	- E.g. Config file missing, defaulting to default settings
- `info`
	- `spdlog::info()`
	- General milestones
	- E.g. User logged in
- `debug`
	- `spdlog::debug()`
	- Info useful for developers
	- E.g. Connected to port ...
- `trace`
	- `spdlog::trace()`
	- Quite low level info relative to the user
	- E.g. The loop is at index 5
#### Setting a Level
##### Per Logger
- Most common
- Each logger only shows specific message, tailored to their purpose
- Initialize
	- `<logger_name>->set_level(spdlog::level::<level>)`
##### Global
- A top level call that effects all loggers
- Initialize
	- `spdlog::set_level(spdlog::level::<level>)`
### Parts
- There are three main components spdlog offers
#### Loggers
- The object called in the code to write logs
- Of the `spd::logger` type
	- It's an object
- Explicitly initializing a logger
	- We often use a smart pointer to manage the logger
	- `auto <name> = std::make_shared<spdlog::logger>(<name>, <sinks_iterators>);`
		- We can pass in the beginning and end iterators of a sink object
		- We use `auto` for quality of life. We could pass in the entire `std::shared_ptr` type but it does not contribute much and just makes it harder to read
	- We can explicitly call loggers to attach it to multiple sinks
- Loggers can also be initialized with a sink attached to it, which is more common. However, how such an action is done differs depending on the type of sink. Thus, we will redirect you to the [[#Sinks|sinks section]] down below
- To log a message, we write `<logger_name>-><level>(<message>)`
	- The message can be done with `{}` syntax
		- E.g. `logger->info("Task {} is {}% complete", task_id, progress);`
#### Formatters
- Control the content and appearence of the message
- The default format of a message is `[YYYY-MM-DD HH:MM:SS.mmm] [logger_name] [log_level] message`
- The format of a message can be customized with `spdlog::set_pattern("[%H:%M:%S %z] [%n] [%^---%L---%$] %v")`
#### Sinks
- Where the messages go
	- E.g. Console, file, network
- A logger can have multiple sinks
- Sinks come with multithreaded and singlethreaded versions, indicated with `_mt` and `_st` suffixes, respectively
	- Multithreaded versions are generally preferred
- Sinks can be be initialized with a logger attached or on their own
- Sinks also have a shortcut way or an explicit way to initialize. Which one to use will depend on the sink and the situation
	- When explicitly initialize, you will have to manually attach the logger to the sink
##### `"spdlog/sinks/stdout_color_sinks.h"` Header
- Writes to terminal
	- With colour! Watch the spelling ...
- Shortcut initialization
	- `auto <logger_name> = spdlog::stdout_color_mt(<logger_name>);`
- Explicit initialization
	- `auto <sink_name> = std::make_shared<spdlog::sinks::<sink_type> >();`
##### `"spdlog/sinks/rotating_file_sink.h"` Header
- Dumps logs into a file, but swaps it out once it reaches a certain size. Keeps a certain amount of files as history
- Shortcut initialization
	- `auto <logger_name> = spdlog::rotating_logger_mt(<logger_name>, <file_name>, <max_file_size_in_bytes>, <max_file_history_size>, <optional_rotate_on_open>);`
- Explicit initialization
	- ```c++
	  auto <logger_name> = std::make_shared<spdlog::sinks::rotating_file_sink_mt>(
		  <file_name>, 
		  <max_file_size_in_bytes>,
		  <max_file_history_size>,
		  <rotate_on_open_boolean> // Optional
	  ); // Don't forget semicolon!
	  ```
- `rotate_on_open` writes to a new file upon restarting the program
##### `"spdlog/sinks/daily_file_sink.h"` Header
- Writes to a new file at a set time during the day every day
- Uses 24-hour time
- Shortcut initialization
	- `auto <logger_name> = spdlog::daily_logger_mt(<logger_name>, <file_name>, <hour>, <minute>, <truncate_boolean>);`
	- Can not adjust file history size
- Manual initialization
	- ```c++
	  auto <logger_name> = std::make_shared<spdlog::sinks::daily_file_sink_mt>(
		  <file_name>, 
		  <hour>, 
		  <minute>,
		  <truncate_boolean>,
		  <file_lifespan_in_days>
	  ); // Semicolon
	  ```
- `<truncate_boolean>` is optional
	- If true, upon restart, wipes current file and starts anew
	- If false or not written, appends messages to current file
##### `"spdlog/sinks/null_sink.h"` Header
- A black void
- When you try to end a message to this sink, no message appears
- Useful if you need to send junk logs somewhere
- Superfast
- Shortcut initialization
	- `auto <logger_name> = spdlog::null_logger_mt(<logger_name>);`
- Manual initialization
	- `auto <sink_name> = std::make_shared<spdlog::sinks::null_sink_mt>();`
