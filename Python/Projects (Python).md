# Structure of the Project
- Generally, we want to have a `src` file that we put all our logic in. Our interface, our logic, but not our tests
# Package Manager
## `pip` Package Manager
- !!!
# Building
## `pyproject.toml` File
- We can create this file the root of our working directory
- This is a standardized way to assist in the building of Python projects
### Introduction
- Requires name and version under `[project]`
- ```toml
  [project]
  name = "my_project"
  version = "0.1.0"
  ```
### Dependencies
- Listed as part of a list under the name `dependencies`
- ```toml
  [project]
  name = "my_project"
  version = "0.1.0"
  dependencies = [
	  "conan>=2.0"
  ]
  ```
- They require a version number
## `pip3 install .` Command
- If our `pyproject.toml` file is configured properly, we should be able to run this command and all dependencies will be properly sorted out
# Documentation
## Docstrings
### Sources
- [Real Python - Guide to Python Documentation](https://realpython.com/documenting-python-code/)
### Introduction
- Docstrings are actually a feature completely native to Python, without requiring an installation from an external source
- Simply open and end a Docstring with triple double quotes:
	- ```python
	  def mySillyMethod(x: int) -> int:
		  """Adds one to the input and returns it.
		  
		  Args:
			  x (int): The input
			  
		  Returns:
			  int: The input increased by one
		  """
		  
		  return x + 1;
	  ```
### Style
- [[Style (Python)|Here]]
# Debugging
## Native
### Introduction
- We can set breakpoints with `breakpoint()` and run our program as per usual
### Methods
- `breakpoint()`
	- Introduced in Python 3.7, you can simply drop this function where you like and it will work as a breakpoint
	- Will not cause the program to immediately enter the debugger, as `set_trace()` from [[#`pdb` Debugger|pdb]] would
### Commands
- [[#`pdb` Debugger#Commands|Here]]
## `pdb` Debugger
- Native
### Introduction
- We can set breakpoints with `set_trace()` and run our program as per usual in the terminal
### Functions
- `set_trace()`
	- Sets a breakpoint and will cause the program to enter the debugger on call
### Commands
- `c` or `cont` or `continue`
	- Continue execution until another breakpoint is encountered
- `d` or `down`
	- !!!
- `h` or `help`
	- On its own
		- Print list of available commands
	- With a command as an argument
		- Print help about that command
- `l` or `list`
	- List code of current file
	- `l` or `list`
		- Without arguments, list 11 lines around the current file
			- Upon continued entry, continue down the file
	- `l .` or `list .`
		- List 11 lines around the current breakpoint
- `p <expression>`
	- Print value of the expression
- `pp <expression>`
	- Pretty print value of the expression
- `q` or `quit` or `exit`
	- Exit
- `s` or `step`
	- Execute current line and stop at the first possible occasion
- `u` or `up`
	- !!!
- `w` or `where`
	- Print a stack trace
## `ipdb` Debugger
- Third party
### Introduction
- Install with `pip install ipdb`
### Functions
- `set_trace()`
	- Sets a breakpoint and will cause the program to enter the debugger on call
### Commands
- [[#`pdb` Debugger#Commands|Here]]
## VsCode
- Third party, technically
- !!!
# Testing
## pyTest
### Sources
- [YouTube - Tech With Tim](https://www.youtube.com/watch?v=EgpLj86ZHFQ)
- [StackOverflow - pytest Not Detecting Tests](https://stackoverflow.com/questions/76580060/pytest-no-tests-ran-even-though-tests-were-clearly-run)
### Set Up
- Install the `pytest` module
- For initialization in `pyproject.toml`:
	- ```toml
	  [tool.pytest.ini_options]
	  pythonpath = ["."]
	  ```
### Introduction
- Super easy to use:
	- Create a test file
		- Import the `pytest` module where needed
		- Import functions or classes you wish to test
		- Write test methods to test behaviour
	- Run the test file in the terminal with `pytest <name_of_test_file>` or `pytest *`. Make sure to specify the directory!
- Suppose a file `operators.py` with functions:
	- ```python
	  def add(x, y):
		  return x + y
	  
	  def subtract(x, y):
		  return x - y
	  ```
- And the test file `test.py`:
	- ```python
	  from source import operators
	  
	  def testAdd():
		  assert 3 == operators.add(1, 2)
		  assert 3 == operators.add(2, 1)
		  assert 5 == operators.add(2, 3)
		  
	  def testSubtract():
		  assert 1 == operators.add(2, 1)
		  assert -1 == operators.add(1, 2)
		  assert 3 == operators.add(5, 2)
	  ```
- Note that pytest is picky with naming; the tests must begin with `test`
### Assertion Types
#### `assert` (Colour)
- The bread and butter for nearly all assertions for testing
- We simply right assert followed by the expression we wish to be true:
	- `assert <expression>`
- We may optionally include a message upon failure
	- `assert <expression>, "<message>"
#### `pytest.approx()` (Colour)
- !!!
#### `pytest.raises()` (Colour)
- `pytest.raises(<exception(s)>)`
	- You have to pass the exceptions as classes
- Returns a context manager
- Used to handle functions that may raise exceptions
- We use a [[Core (Python)#`with` Keyword|with]] statement to open up a testing block:
	- ```python
	  def testMethod(vehicle: Vehicle):
		  with pytest.raises(InvalidGasException):
			  vehicle.addGas(0)
	  ```
	- We write the faulty code in the block below
- We can include multiple exceptions:
	- ```python
	  def testMethod(car: Car):
		  with pytest.raises(InvalidGasAmountException, AddZeroGasException):
			  car.addGas(0)
	  ```
- If the indicated exception or exceptions or not raised, `pytest` will raise an error
### Decorators
#### `@pytest.fixture()` (Colour)
- Upon decorating a method with this decorator, the function will run before any required test method within the scope
- We specify the scope with `scope="<scope>"` and insert it as an argument
	- By default, the scope is "function", which means for each test method the pytest.fixture method will run
- Pytest matches function objects returned by the decorated method to the correct argument name by whether the name is the same
	- This will work
		- ```python
		  @pytest.fixture		  
		  def vehicle():
			  return Vehicle(50)
		  
		  def testAddGasOne(vehicle: Vehicle):
			  vehicle.addGas(1)
			  
			  assert 1 == vehicle.getCurrentGasAmount()
		  ```
	- This will not
		- ```python
		  @pytest.fixture
		  def vehicleA():
			  return Vehicle(50)
		  
		  def testAddGasOne(vehicle: Vehicle):
			  vehicle.addGas(1)
			  
			  assert 1 == vehicle.getCurrentGasAmount()
		  ```
			- Because the names are not exactly the same
	- You can pass certain objects to certain test methods using this idea
		- ```python
		  @pytest.fixture		  
		  def vehicle():
			  return Vehicle(50)
		  
		  @pytest.fixture		  
		  def vehicleSpecial():
			  return Vehicle(2)
			  
		  def testAddGasOne(vehicle: Vehicle):
			  vehicle.addGas(1)
			  
			  assert 1 == vehicle.getCurrentGasAmount()
		  
		  def testAddGasOneToSpecial(vehicleSpecial: Vehicle):
			  vehicleSpecial.addGas(1)
			  
			  assert 1 == vehicleSpecial.getCurrentGasAmount()
		  ```
			- Both tests will pass
#### Marking with`@pytest.mark`
##### Sources
- [Documentation](https://docs.pytest.org/en/stable/example/markers.html)
- [YouTube - BugBytes](https://www.youtube.com/watch?v=7mFQsv2NBG8)
##### Builtins
- You can run `pytest --markers` to view all built in markers
###### `@pytest.mark.parametrize()` Decorator
- Sources
	- [Documentation - Function Signature](https://docs.pytest.org/en/stable/reference/reference.html#pytest.Metafunc.parametrize)
	- [Documentation - How to Parametrize](https://docs.pytest.org/en/stable/how-to/parametrize.html#parametrize)
	- [Documentation - Parametrize](https://docs.pytest.org/en/stable/example/parametrize.html)
- Signature: `parametrize(argnames: str | Sequence[str], argvalues: Iterable[Sequence[object] | object])
- We can pass in our parameters in the decorator and decorate a generalized test method
- This allows us to not have to copy paste a bunch of assert statements
- ```python
  import pytest
  
  from operators import add
  
  @pytest.mark.parametrize(("x", "y", "expected"), [
	  (-2, -1, -3),
	  (-1, -2, -3),
	  (-1, -1, -2),
	  (-2, 3, 1),
	  (3, -2, 1),
	  (-3, 2, -1),
	  (2, -3, -1),
	  (0, 0, 0),
      (0, 1, 1),
	  (1, 0, 1),
	  (1, 1, 2),
	  (1, 2, 3),
	  (2, 1, 3),
  ])
  def testAdd(x: int, y: int, expected: int) -> None:
	  assert add(x, y) == expected
  ```
##### Custom Marks
- Custom markers can be used to mark test for filtering and and choosing to run only certain types of tests
###### Registering Custom Markers
- !!!!
### Fixtures
#### `monkeypatch` Fixture
##### Sources
- [Pytest Documentation - How To monkeypatch](https://docs.pytest.org/en/stable/how-to/monkeypatch.html)
##### Introduction
- !!!
##### Methods
- !!!
##### Example
- !!!
### Parameterization
- [[#`@pytest.mark.parametrize()` Decorator|Here]]
### Example
- ```python
  from source.VehicleModule import Vehicle, InvalidGasAmountException, TooMuchGasException
  
  import pytest
  
  MAX_GAS_AMOUNT = 50
  
  def assertNoChange(testMethod):
	  def wrapper(vehicle):
		  _assertNoGas(vehicle)
		  testMethod(vehicle)
		  _assertNoGas(vehicle)
	  
	  return wrapper
  
  @pytest.fixture
  def vehicle()
	  return Vehicle(MAX_GAS_AMOUNT)
  
  @assertNoChange
  def testAddGasNegativeAmount(vehicle: Vehicle):
	  with pytest.raises(InvalidGasAmountException):
		  vehicle.addGas(-1)
  
  @assertNoChange
  def testAddGasZero(vehicle: Vehicle):
	  with pytest.raises(InvalidGasAmountException):
		  vehicle.addGas(0)
  
  def testAddGasOne(vehicle: Vehicle):
	  _assertMatchAmount(vehicle, 1)
	  
  def testAddGasMaxAmountMinusOne(vehicle: Vehicle):
	  _assertMatchAmount(vehicle, MAX_GAS_AMOUNT - 1)
  
  def testAddGasMaxAmountMinusOne(vehicle: Vehicle):
	  _assertMatchAmount(vehicle, MAX_GAS_AMOUNT)
	  
  @assertNoChange
  def testAddGasMaxAmountMinusOne(vehicle: Vehicle):
	  with pytest.raises(TooMuchGasException):
		  _assertMatchAmount(vehicle, MAX_GAS_AMOUNT + 1)
	  
  def _assertMatchAmount(vehicle: Vehicle, amount):
	  _assertNoGas(vehicle)
	  
	  vehicle.addGas(amount)
	  
	  assert amount == vehicle.getCurrentGasAmount()
  
  def _assertNoGas(vehicle: Vehicle):
	  assert 0 == vehicle.getCurrentGasAmount()
  ```
	- We specify the type of each `vehicle` parameter so that VSCode gives us the dropdown menu when we attempt to operate on `vehicle`
		- This is because Pytest knows how to properly link the objects given from pytest.fixture methods but not native IDE's
- Relevant tested code
	- ```python
	  class Vehicle:
		  def __init__(self, gas_max):
			  self._gas_max = gas_max
			  
			  self._gas_current = 0
		  
		  def addGas(self, gas):
			  if (gas <= 0):
				  raise InvalidGasAmountException()
			  
			  if (self._gas_current + gas > self._gas_max):
				  raise TooMuchGasException()
			  
			  self._gas_current += gas
			  
		  def getCurrentGasAmount(self):
			  return self._gas_current
	  
	  class InvalidGasAmountException(Exception):
		  def __init__(self):
			  super().__init__()
	  
	  class TooMuchGasException(Exception):
		  def __init__(self):
			  super().__init__()
	  ```
## pyTest-asyncio
### Sources
- [PyPi](https://pypi.org/project/pytest-asyncio/)
### Installation
- `pip install pytest-asyncio`
### Introduction
- Native pyTest is insufficient to run tests that call asynchronous functions. Thus, we require pyTest-asyncio
- Generally, we just mark asynchronous methods with the `@pytest.mark.asyncio` [[#`@pytest.mark.asyncio` Decorator|decorator]]
### Decorators
#### `@pytest.mark.asyncio` Decorator
- Indicates that a test method is asynchronous
#### `@pytest_asyncio.fixture` Decorator
- !!!
### Usage Example
- ```python
  import asyncio
  
  from unittest.mock import AsyncMock, MagicMock
  
  import pytest
  
  from pytest_mock import MockerFixture
  
  from src.source_bot.scraping import ScraperBot
  
  @pytest.fixture
  def scraper_bot() -> ScraperBot:
	  DUMMY_NUMBER = 0
	  
	  return ScraperBot(DUMMY_NUMBER)
  
  @pytest.mark.asyncio
  async def test_fake_set_guild(mocker: MockerFixture, scraper_bot: ScraperBot) -> None:
	  mock_guild: MagicMock = mocker.MagicMock()
	  mock_fetch_guild: AsyncMock = mocker.patch("discord.Client.fetch_guild")
	  
	  mock_fetch_guild.return_value = mock_guild
	  
	  await scraper_bot.fake_set_guild()
	  
	  assert scraper_bot.fake_get_guild == mock_guild
  ```
## pyTest-Mock
### Sources
- [YouTube - Tech with Tim - Pytest Tutorial](https://www.youtube.com/watch?v=EgpLj86ZHFQ)
- [Datacamp](https://www.datacamp.com/tutorial/pytest-mock)
### Installation
- `pip install pytest-mock`
### Introduction
- A thin wrapper over the [[#`unittest` Module#`mock` Module|unittest.mock]] module
- It allows us to avoid a lot of boilerplate and manual management required if we were to use the `unittest.mock` module to create mocks
### Fixtures
#### `mocker` Fixture
##### Introduction
- A [[#`MockerFixture` Class|MockerFixture]]
- A `mocker` is created via a `@pytest.fixture` when needed
- `mocker` is an interface from which we can access factory methods to create classes from the [[#`unittest` Module#`mock` Module|unittest.mock]] module
##### Methods
- `AsyncMock()`
	- Creates an [[#`unittest` Module#`mock` Module#Classes#`AsyncMock` Class|AsyncMock]]
- `MagicMock()`
	- Creates a [[#`unittest` Module#`mock` Module#Classes#`MagicMock` Class|MagicMock]]
- `Mock()`
	- Creates a [[#`unittest` Module#`mock` Module#Classes#`Mock` Class|Mock]]
- `patch()`
	- Behaves like [[#`unittest` Module#`mock` Module#Methods|patch]]
##### Usage Example
- ```python
  import asyncio
  
  from unittest.mock import AsyncMock, MagicMock
  
  import pytest
  
  from pytest_mock import MockerFixture
  
  from src.source_bot.scraping import ScraperBot
  
  @pytest.fixture
  def scraper_bot() -> ScraperBot:
	  DUMMY_NUMBER = 0
	  
	  return ScraperBot(DUMMY_NUMBER)
  
  @pytest.mark.asyncio
  async def test_fake_set_guild(mocker: MockerFixture, scraper_bot: ScraperBot) -> None:
	  mock_guild: MagicMock = mocker.MagicMock()
	  mock_fetch_guild: AsyncMock = mocker.patch("discord.Client.fetch_guild")
	  
	  mock_fetch_guild.return_value = mock_guild
	  
	  await scraper_bot.fake_set_guild()
	  
	  assert scraper_bot.fake_get_guild == mock_guild
  ```
	- We can create mocks using the factory methods
	- We can modify `<mock>.return_value` to control the return type of a function we wish to patch
		- `<mock>.return_value` returns another `Mock`
	- In the source file I call `super().fetch_guild(guild_id)`. Because I call with super, which leads to `discord.Client`, my path is as such. Otherwise if I call with `self`, then I'd write `src.source_bot.scraping.ScraperBot.fetch_guild`
- You can actually mock network calls
- ```python
  ```
### Classes
#### `MockerFixture` Class
- !!!
## `unittest` Module
### `mock` Module
#### Sources
- [Documentation](https://docs.python.org/3/library/unittest.mock.html)
- [Documentation - Getting Started](https://docs.python.org/3/library/unittest.mock-examples.html)
- [Real Python - What is Mocking?](https://realpython.com/python-mock-library/#what-is-mocking)
- [YouTube - pixegami - Pytest Tutorial](https://www.youtube.com/watch?v=YbpKMIUjvK8)
- [YouTube - redshiftzero - How to Use Python's unittest.mock.patch](https://www.youtube.com/watch?v=WFRljVPHrkE)
#### Introduction
- A module that offers tools to help mock
- Mocking is when we fake a function or class and create a custom implementation of it
- We mock external dependencies such that we can control their behaviour for testing. Examples of such dependencies include:
	- Databases
	- Disk IO operations
	- Network calls
	- HTTP network requests
	- API calls
#### Methods
- `patch(target: str, new=DEFAULT, spec=None, create=False, spec_set=None, autospec=None, new_callable=None, *, unsafe=False, **kwargs)`
	- What patch does is create a mock of `target`, which is the string of a target, which can be a functions, class, or module
	- Defaults to `MagicMock`
		- Will use `AsyncMock` for aysnchronous functions
	- The golden rule for naming your target is: patch where the target is used not where it's defined
		- Name your target with the path that leads to its usage
		- [[#`mocker` Fixture#Usage Example|Example]] here. It's with `mocker` but it's similar enough
#### Classes
##### `AsyncMock` Class
- Inherits from
	- [[#`Mock` Class|Mock]]
	- !!!
##### `CallableMixin` Class
- !!!
##### `MagicMock` Class
- Inherits from
	- [[#`Mock` Class|Mock]]
	- !!!
##### `Mock` Class
- Inherits from 
	- [[#`CallableMixin` Class|CallableMixin]]
	- [[#`NonCallableMock` Class|NonCallableMock]]
##### `NonCallableMock` Class
- !!!
#### Decorators
- `@patch`
	- !!!
#### Usage
##### Context Manager
- !!!
##### Decorator
- !!!
##### Inline
- !!!
# Logging
- Sources
	- [Tech With Tim](https://www.youtube.com/watch?v=urrfJgHwIJA)
### Variables
- `DEBUG`
	- 10
- `INFO`
	- 20
- `WARNING`
	- 30
- `ERROR`
	- 40
- `CRITICAL`
	- 50
### Functions
- `getLogger()
	- !!!
### Classes
#### `FileHandler` Class
- From [[#`Handler` Class|Handler]]
##### Initialization
- `<name> = logging.FileHandler(<file>)`
	- A string or `Path` object; [[#`Path` Class|Path]]
#### `Formattter` Class
##### Introduction
- Converts a [[#`LogRecord` Class|LogRecord]] into a human or external system readable output string
##### Initialization
- `<name> = logging.Formatter()`
	- Default: `Formatter(fmt=None, datefmt=None, style='%', validate=True, *, defaults=None)`
		- `fmt`
			- A format string
			- Mapping keys can be found [[#`LogRecord` Class#Attributes|here]]
		- `datefmt`
			- A format string for the date and time portion of the string
		- `style`
			- One of
				- `%`
				- `{`
				- `$`
			- Determines how `fmt` will be formatted with the mapping keys
		- `validate`
			- If true, incorrect or mismatched `fmt` and `style` will raise a `ValueError`
		- `defaults`
			- !!!
#### `Handler` Class
- `setFormatter(<Formatter>)`
	- Sets the [[#`Formattter` Class|Formatter]]
- `setLevel(<level>)`
	- Sets the level
	- Can be used to further filter logs that pass through logger
#### `Logger` Class
- `addHandler(<Handler>)`
	- Adds handler
- `debug(<message>)`
- `info(<message>)`
- `setLevel(<level>)`
	- Sets the level for the logger
	- Only logs at or above the level will pass
#### `LogRecord` Class
##### Attributes
- `asctime`
	- `%(asctime)s`
	- Human readable time when the `LogRecord` was created
	- By default, `2003-07-08 16:49:45,896`
- `filename`
	- `%(filename)s`
- `funcName`
	- `%(funcName)s`
- `levelname`
	- `%(levelname)s`
- `lineno`
	- `%(lineno)d`
- `message`
	- `%(message)s`
	- Log message
- `module`
	- `%(module)s`
- `name`
	- `%(name)s`
	- Name of the logger
- `process`
	- `%(process)d`
	- Process ID
- `processName`
	- `%(processName)s`
- `thread`
	- `%(thread)d`
	- Thread ID
- `threadName`
	- `%(threadName)s`
### Usage
- ```python
  import logging
  
  from pathlib import Path
  
  def doSmth(logger: logging.Logger) -> None:
	  for i in range(11):
		  logger.info(i)
  
  def main() -> None:
	  logger = logging.getLogger(__name__)
	  logger.setLevel(logging.INFO)
	  handler = logging.FileHandler(log)
	  formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
	  handler.setFormatter(formatter)
	  logger.setHandler(handler)
	  
	  doSmth(logger)
	  
  if __name__ == "__main__":
	  main()
  ```
	- It's customary to name the logger after the module
	- It's customary to have one logger per module
