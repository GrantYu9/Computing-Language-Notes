# Standard Library
## `abc` Module
- !!!
## `asyncio` Module
- Sources
	- [Tech With Tim - Asyncio in Python](https://www.youtube.com/watch?v=Qb9s3UiMSTA)
	- [Python Documentation - Event Loop](https://docs.python.org/3/library/asyncio-eventloop.html)
	- [Python Documentation - Asyncio](https://docs.python.org/3/library/asyncio.html)
	- [Geeks for Geeks - TaskGroup](https://www.geeksforgeeks.org/python/python-taskgroups-with-asyncio/)
### Introduction
#### Event Loop
- The way Python runs asynchronous functions using the `asyncio` module is built on the idea of the event loop
- The event loop can be thought of as a circle, with tasks waiting outside the circle to be run. When ready, a single task can be run inside the circle. If we need to pause the task, we'll put it aside in the circle and bring another task into the center of the circle, repeating until all tasks are done
- Coroutines are not ran in the event loop
#### Coroutines vs Tasks
- A coroutine is written with the `async` and `await` keywords and simply trying to call it will not execute; it must be awaited
- A task is a wrapped coroutine designed to be ran concurrently in the event loop
	- Simply creating it will initiate execution
#### The Function of `await`
- `await` literally just pauses execution for a coroutine or a task to finish
### Functions
- `create_task(<coroutine>)`
	- Creates a [[#`Task` Class|task]]
	- Requires a coroutine as a parameter
	- When we `await` a task, it will put that task into the event loop
		- Execution will continue until all awaited tasks in a block are completed
		- ```python
		  import asyncio
		  
		  from random import random
		  
		  async def fetch_data(sleep_time: int) -> float:
			  print("Initiating.")
			  await asynco.sleep(sleep_time)
			  number = random()
			  print(f"Done. {number}.")
			  return number
			  
		  async def main() -> None:
			  task_1 = asyncio.create_task(fetch_data(2))
			  task_2 = asyncio.create_task(fetch_data(2))
			  
			  result_1 = await task_1
			  result_2 = await task_2
			  
			  task_3 = asyncio.create_task(fetch_data(2))
			  
			  result_3 = await task_3
			  
			  print(result_1, result_2, result_3)
		  
		  if __main__ == "__main__":
			  asyncio.run(main())
		  ```
			- This will execute `task_1` and `task_2` concurrently but `task_3` is run later
- `gather(<coroutines>)`
	- Wraps coroutines as tasks, executes them, and returns the answers as a list in the same respective order as the arguments
	- The problem with this method comes when we try to handle exceptions
		- By default, there is a boolean `return_exceptions` which is set to `False` by default. Thus, any coroutine that raises an exception will cause the `gather()` to fail immediately. This is intended fail-fast behaviour
		- The common "workaround" is to enable `return_exceptions` to `True` as a [[Core (Python)#Keyword Arguments|keyword argument]]. The prolbem is, exceptions are now included in the return list and programmers often have to parse it for exceptions, which is considered poor practice
		- The modern solution is to use [[#`TaskGroup` Class|TaskGroup]]
- `run(<coroutine>)`
	- Wraps the coroutine as a task, runs the task in an event loop, and returns the result
- `sleep(<number>)`
	- Suspends the coroutine for a specified amount of time in seconds
### Classes
#### `Condition` Class
- !!!
#### `Event` Class
##### Introduction
- Essentially an on or off switch
- Blocked by default
##### Initialization
- `<name> = asyncio.Event()`
##### Methods
- `clear()`
- `is_set()`
- `set()`
- `wait()`
##### Usage
- Can be used to signal others to wait until the `Event` is unblocked, like a gateway
- ```python
  import asyncio
  
  async def startUp(event: asyncio.Event) -> None:
	  await asyncio.sleep(1) # Dummy IO work
	  
	  event.set()
	  
	  print("Event set.")
  
  async def worker(event: asyncio.Event) -> None:
	  print("Worker notified.\nWaiting for event.")
	  
	  await event.wait()
	  
	  print("Worker finished.")
	  
	  event.clear()
  
  async def main() -> None:
	  event = asyncio.Event()
	  
	  await asyncio.gather(startUp(event), worker(event))
  
  if __name__ == "__main__":
	  asyncio.run(main())
  ``` 
#### `Lock` Class
##### Introduction
- We use the lock to allow only one coroutine to modify shared resource(s) at a time
- It's a context manager
##### Initialization
- `<name> = asyncio.Lock()`
##### Usage
- We use it with `async with` as a context manager
- We only use it when needed, in a critical phase, when we have to interact with with shared resources(s)
	- Otherwise, we'd be wasting the advantages of asynchronous programming
- An example of proper implementation:
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
		  
		  await asyncio.gather(*(increment(shared_counter, lock) for i in range(3)))
	  
	  if __name__ == "__main__":
		  asyncio.run(main())
	  ```
		- We use a list because Python `int`s are immutable
		- We only use the lock for the critical phase when we need to modify the shared resource, and we take advantage of asynchronous programming to efficiently start waiting for all the tasks at the same time, as we do not put a lock on that part
- An example of poor implementation:
	- ```python
	  import asyncio
	  
	  async def increment(shared_counter: list, lock: asyncio.Lock) -> None:
		  print("Initiating increment.")
		  
		  async with lock:
			  print("Lock acquired.")
			  
			  await asyncio.sleep(1)
			  
			  shared_counter[0] += 1
			  
			  print(f"Increment completed. Shared counter is now: {shared_counter[0]}.")
		  
	  async def main() -> None:
		  shared_counter = [0]
		  lock = asyncio.Lock()
		  
		  await asyncio.gather(*(increment(shared_counter, lock) for i in range(3)))
	  
	  if __name__ == "__main__":
		  asyncio.run(main())
	  ```
		- Now, every time we get the lock we have to wait a bit, instead waiting outside the lock
#### `PriorityQueue` Class
- !!!
#### `Queue` Class
- Sources
	- [StackOverflow](https://stackoverflow.com/questions/49637086/python-what-is-queue-task-done-used-for)
##### Introduction
- Used to safety transport and process data from one point to another in the program
##### Initialization
- `<name> = ascynio.Queue(<int>)`
	- By default to be 0
	- If a negative integer is inputted, size will be unbounded
##### Methods
- `empty()`
	- Return true if queue is empty. Else, return false
- `full()`
	- Return true if there are `maxsize` items in the queue
	- If queue was initialized to 0 then this never returns true
- `async get()`
	- Remove and return an item from the queue
- `get_nowait()`
	- Return an item if one is immediately available, else raise `QueueEmpty`
- `async join()`
	- Block until all items in the queue have been received and processed
	- Count of unprocessed tasks goes up whenever an item is added to the queue. This number only goes down with calls of `task_done()`. When the count of unprocessed tasks hits 0, `join()` unblocks
- `maxsize()`
	- Return number of items allowed in queue
- `async put(<item>)`
	- Put an item
- `shutdown()`
	- !!!
- `qsize()`
	- Returns number of items in the queue
- `task_done()`
	- Indicate that an item in the queue is processed. Only useful with `join()`
##### Usage
- Consider the following example, which will illustrate many points:
	- ```python
	  import asyncio
	  
	  async def producer(queue: asyncio.Queue[str], item: str) -> None:
		  await queue.put(item)
	  
	  async def consumer(queue: asyncio.Queue[str]) -> None:
		  while True:
			  item = await queue.get()
			  
			  print(item)
			  
			  queue.task_done()
		  
	  async def main() -> None:
		  queue: asyncio.Queue[str] = asyncio.Queue(5)
		  
		  asyncio.create_task(consumer(queue)) # Background task
		  
		  items = ["Hello", "world", "with", "asyncio"]
		  
		  await asyncio.gather(*(producer(queue, items[i]) for i in range(len(items))))
		  
		  await queue.join() # Block and wait for processing
		  
		  print("Yay")
	  
	  if __name__ == "__main__":
		  asyncio.run(main())
	  ```
		- We specify a queue, start a background process of consumer without awaiting, and pass queue to it
		- When then pass our items to the producer and it puts it in the queue
		- Then we block with join so all the items can be processed properly before "Yay" is printed. If we comment out the join, only "Hello" will print followed by "Yay", and the program will terminate, because only one task will be done in the event loop
#### `Semaphore` Class
##### Introduction
- Like a [[#`Lock` Class|lock]], but allows for multiple coroutines to access a shared resource
- Good for throttling
- Manages an internal counter
	- When a task needs to use the semaphore, `acquire()` is called and the count is decremented
	- When the task is not using it, `release()` is called and the count is increased
	- The count can never go below 0
##### Initialization
- `<name> = asyncio.Semaphore(<number>)`
	- By default to be $1$, so like a lock
	- Parameter actually optional
##### Usage
- Improperly using semaphores can easily introduce race condition and concurrency errors, especially when trying to modify shared resources:
	- ```python
	  import asyncio
	  
	  async def increment(shared_counter: list, semaphore: asyncio.Semaphore) -> None:
		  print("Initiating increment.\n")
		  
		  await asyncio.sleep(1)
		  
		  async with semaphore:
			  print("Semaphore acquired.\n")
			  current = shared_counter[0]
			  await asyncio.sleep(1)
			  shared[0] = current + 1
			  print(f"Increment completed.\nSemaphore released.\nShared counter is now {shared_counter[0]}.\n")
	  
	  async def main() -> None:
		  semaphore = asyncio.Semaphore(2)
		  shared_counter = [0]
		  
		  await asyncio.gather(*(increment(shared_counter, semaphore) for i in range(3)))
	  
	  if __name__ == "__main__":
		  asyncio.run(main())
	  ```
- A better use would be to use a semaphore to throttle resources:
	- ```python
	  import asyncio
	  
	  async def replaceValue(semaphore: asyncio.Semaphore, array: list, index: int, value: int, id: int) -> None:
		  print(f"Function called. ({id})\n")
		  
		  async with semaphore:
			  print(f"Semaphore acquired. ({id})\n")
			  
			  await asyncio.sleep(1)
			  
			  array[index] = target_value
			  
			  print(f"Semaphore released. ({id})\n")
		  
		  print(f"Function complete. ({id})\n")
	  
	  async def main() -> None:
		  array = [i for i in range(3, 14)]
		  semaphore = asyncio.Semaphore(3)
		  
		  print(f"Before: {array}.\n")
		  
		  await asycnio.gather(*(replaceValue(semaphore, array, i, array[i] + 1, i + 1) for i in range(11)))
		  
		  print(f"After: {array}.\n")
		  
	  if __name__ == "__main__":
		  asyncio.run(main())
	  ```
		- We limit only 3 coroutines to do their work instead of all 11 at once
		- There is no race condition because they each modify their own section of the list
#### `Task` Class
##### Introduction
- A task can be thought of as a wrapped coroutine object
- Tasks are what actually allow for the asynchronous capabilities that `asyncio` offers and are what run in the event loop
##### Methods
- `cancel()`
	- Request the task to be cancelled
	- If task is done or cancelled, return false. Otherwise, return true
- `cancelled()`
	- Return true if task is cancelled
- `done()`
	- Return true if task is done
	- Task is done when either
		- A value has been a returned
		- An exception has been raised
		- Or the task has been cancelled
- `exception()`
	- Returns exception of the task
	- If no exception, returns `None`
	- If the Task has been cancelled, a `CancelledError` exception will be raised
	- If the Task's result is not available yet, an `InvalidStateError` exception will be raised
- `get_coro()`
	- Returns the coroutine object wrapped within
- `result()`
	- Returns the result of the Task
	- If the Task has been cancelled, a `CancelledError` exception will be raised
	- If the Task's result is not available yet, an `InvalidStateError` exception will be raised
- `uncancel()`
	- !!!
#### `TaskGroup` Class
- Requires an understanding of [[Core (Python)#Exception Groups & `except*` Keyword|exception groups]]
##### Introduction
- Throws an ExceptionGroup upon failure of any tasks
- Because we're are running objects concurrently, multiple exceptions can be thrown at the same time
- A context manager
##### Methods
- `create_task()`
	- The same as `create_task()` in [[#`asyncio` Module#Functions|asyncio]] module but further managed by the task group
	- Returns a task
##### Usage
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
## `base64` Module
- `base64.b64encode(<value>)`
	- Encodes from bytes to base 64
- `<variable>b64becode(<type>)`
	- Decodes from base64 to a type, such as ASCII
## `builtins` Module
- Always secretly autoimported
### Functions
- `breakpoint()`
	- [[Projects (Python)#Debugging#Native Tools|Here]]
- `getattr()`
	- [[Core (Python)#`getattr()` Function|Here]]
- `len()`
	- !!!
- `open()`
	- By default: `open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`
	- Context manager
	- Modes
		- `r`: Read. Default
		- `w`: Writing. Truncation
		- `a` Writing. Appending
		- `b`: Binary
- `next()`
	- !!!
- `pow`
	- !!!
- `range()`
	- !!!
- `read()`
	- Default: `read(size=-1, /)`
	- Read up to `size` data from file
- `split()`
	- Method within the `str` class
- `write()`
	- Default: `write(data, /)`
- `zip`
	- Takes the first items from each container, forms a tuple, then takes the next items in each list
	- `zip(<container1>, <container2>, ... , <containern>)`
### Classes
#### `Exception` Class
- !!!
#### `ExceptionGroup` Class
- Implements from base [[Libraries (Python)#`Exception` Class|Exception]] class
##### Introduction
- It can be thought of as a container for exceptions
- We can nest exception groups in exception groups
##### Constructor
- `exception_group = ExceptionGroup("<message>", <exeptions>)`
	- Where `<exceptions>` is a list
	- You can put in the same exception again and again
##### Members
- `exceptions`
	- A tuple of exceptions the exception group holds
## `collections` Module
### Classes
- `Counter`
	- !!!
### Modules
#### `abc` Module
##### Classes
###### `Coroutine` Class
- !!!
###### `Generator` Class
- !!!!
## `contextlib` Module
### Decorators
- `asynccontextmanager`
	- !!!
## `datetime` Module
### Attributes
- `MINYEAR = 1`
- `MAXYEAR = 9999
### Classes
#### `date` Class
##### Initialization
- `date(year: int, month: int, day: int)`
	- `MINYEAR <= year <= MAXYEAR`
	- `1 <= month <= 12`
	- `1 <= day <= number of days in the given month and year`
##### Attributes
- `day`
- `month`
- `year`
##### Methods
- `isoformat()`
	- Return a string representing the date in ISO 8601 format
		- `YYYY-MM-DD`
- `fromisoformat(date_string: str)`
	- Return a `date` from a `date_string` in any valid ISO 9601 format, with the following exceptions:
		- !!!
- `fromtimestamp(timestamp: int, tz=None)`
	- Convert UNIX time to `date`
- `timestamp()`
	- Convert `date` to UNIX time
- `today()`
	- Return the current local date
#### `datetime` Class
##### Initialization
- `datetime(year, month, date, hour=0, minute=0, second=0, microsecond=0, tzinfo=None, *, fold=0)`
	- `MINYEAR <= year <= MAXYEAR`
	- `1 <= month <= 12`
	- `1 <= day <= number of days in the given month and year`
	- `0 <= hour < 24`
	- `0 <= minute < 60`
	- `0 <= second < 60`
	- `0 <= microsecond < 1000000`
	- `fold` in `[0, 1]`
##### Attributes
- `day`
- `fold`
- `hour`
- `microsecond`
- `minute`
- `month`
- `second`
- `year`
##### Methods
- `date()`
	- Return date object with same year, month, and day
- `isoformat(sep='T', timespec='auto)`
	- Return a string representing the date and time in ISO 8601 format
		- `YYYY-MM-DDTHH:MM:SS.ffffff` if microsecond is not 0
		- `YYYY-MM-DDTHH:MM:SS` if microsecond is 0
- `fromisoformat(datetime_string: str)`
	- Return a `datetime` from a `datetime_string` in any valid ISO 9601 format, with the following exceptions:
		- !!!
- `fromtimestamp(timestamp: int, tz=None)`
	- Convert UNIX time to `datetime`
- `time()`
	- Return time object with same hour, minute, second, microsecond, and fold
- `timestamp()`
	- Convert `datetime` to UNIX time
- `today()`
	- Return the current local date and time
#### `time` Class
##### Initialization
- `time(hour=0, minute=0, second=0, microsecond=0, tzinfo=None, *, fold=0)`
	- `0 <= hour < 24`
	- `0 <= minute < 60`
	- `0 <= second < 60`
	- `0 <= microsecond < 1000000`
	- `fold` in `[0, 1]`
##### Attributes
- `fold`
- `hour`
- `microsecond`
- `minute`
- `second`
##### Methods
- `isoformat(timespec='auto)`
	- Return a string representing the time in ISO 8601 format
		- `HH:MM:SS.ffffff` if microsecond is not 0
		- `HH:MM:SS` if microsecond is 0
- `fromisoformat(time_string: str)`
	- Return a `time` from a `time_string` in any valid ISO 9601 format, with the following exceptions:
		- !!!
### Operations
- You can generally perform math and conditionals as you'd expect with date/time objects
## `enum` Module
### Methods
- `auto()`
	- Automatically assigns a number for an enum
### Classes
#### `Enum` Class
#### `StrEnum` Class
## `fractions` Module
### Classes
#### `Fraction` Class
- !!!
## `functools` Module
### Classes
#### `Reduce` Class
- !!!
## `io` Module
- !!!
## `inspect` Module
- Sources
	- [W3 Schools](https://www.w3schools.com/python/ref_module_inspect.asp)
	- [Documentation](https://docs.python.org/3/library/inspect.html)
### Introduction
- Allows us to inspect things such as modules, classed, and functions
### Methods
- `getdoc(<object>)`
- `getmembers(<object>)`
	- !!!
- `getsource(<object>)`
- `isbuiltin(<object>)`
- `isclass(<object>)`
- `iscoroutine(<object>)`
- `isfunction(<object>)`
- `isgenerator(<object>)`
- `ismodule(<object>)`
- `signature(<callable>)`
	- Returns a [[#`Signature` Class|Signature]] class of the callable
### Classes
#### `Signature` Class
- !!!
### Usage Example
- ```python
  import inspect
  
  def main() -> None:
	  print(inspect.getdoc(len))
  
  if __name__ == "__main__":
	  main()
  ```
## `itertools` Module
### Classes
#### `Cycle` Class
- !!!
## `json` Module
- Sources
	- [Tech With Tim](https://www.youtube.com/watch?v=-51jxlQaxyA)
### Introduction
- Used with file IO modules to read and write to JSON files
### Functions
- `dump(obj: object, fp, *, skipKeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)`
	- `indent: int | str | None`
	- Writing to a file
- `dumps()`
	- Serializes an object to a JSON formatted string
	- Default: `dumps(obj, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)`
		- `indent`
			- Allows for an indentation amount
		- `sort_keys`
			- Sort key names
	- Writing to a string
- `load()`
	- Reading from a file
- `loads()`
	- Reading from a string
### Examples
- ```python
  import json
  
  from pathlib import Path 
  
  def main() -> None:
	  target: Path = Path(__file__).parent / "target.json"
	  
	  data: dict[str, str | int] = {
		  "food": "noodles",
		  "amount": 2
	  }
	  
	  with target.open(mode='w') as file:
		  json.dump(data, file, indent=4)
  
  if __name__ == "__main__":
	  main()
  ```
- ```python
  import json
  
  from pathlib import Path
  
  def main() -> None:
	  target: Path = Path(__file__).parent / "target.json"
	  
	  with target.open(mode='r') as file:
		  data: str = json.load(file)
  ```
## `logging` Module
- [[Projects (Python)#Logging|Here]]
## `os` Module
### Objects
#### `environ` Object
- A dictionary object that stores all key value pairs of environment variables
## `operator` Module
### Classes
#### `xor` Class
- !!!
## `pathlib` Module
- Sources
	- [YouTube - PyCharm](https://www.youtube.com/watch?v=YwhOUyTxXVE)
	- [YouTube - Corey Schafer](https://www.youtube.com/watch?v=yxa-DJuuTBI)
### Tools
#### `/` Operator
- We use it to create file names
- ```python
  from pathlib import Path
  
  def main() -> None:
	  project_root = Path(__file__)
  
  if __name__ == "__main__":
	  main()
  ```
### Classes
#### `Path` Class
##### Initialization
- `<name> = Path()` or `<name> = Path('.')`
	- Makes `Path` object of current directory 
- `<name_variable> = Path(<name_path>)`
	- Makes `Path` object of the given path name
	- If it starts with `/`, it will assume it's absolute. Else, it will asume it's relative to the 
##### Members
- `name`
	- Filename with extension
- `parent`
	- Directory file is in
- `stem`
	- Filename without extension
- `suffix`
	- File extension
##### Methods
- `absolute()`
	- Returns absolute path
- `exists()`
	- Returns true if file or directory exists
- `is_dir()`
- `is_file()`
- `open(mode='r', buffering=-1, encoding=None, errors=None, newline=None)`
	- Modes
		- `'a'`
			- Write only
			- Append mode
		- `'r'`
			- Read only
		- `'r+'`
			- Read and write
		- `'w'`
			- Write only
			- Override mode
	- Context manager
	- Opens file as a file object
	- Operates like `open()` in [[#`builtins` Module|builtins]]
- `resolve()`
	- !!!
##### Usage
- ```python
  from pathlib import Path
  
  def main() -> None:
	  project_root = Path(__file__).parent.parent.parent
	  
	  target_file = project_root / "actual_txt.txt"
	  
	  with target_file.open(mode='w') as file:
		  file.write("Hello world.")
	  
  if __name__ == "__main__":
	  main()
  ```
## `pdb` Module
- [[Projects (Python)#`pdb` Debugger|Here]]
## `queue` Module
- !!!
## `math` Module
### Types
- !!!
### Methods
- `ceil()`
	- !!!
- `floor()`
	- !!!
## `multiprocessing` Module
- !!!
## `random` Module
### Methods
- `choice(<sequence>)`
	- Returns a random element from the sequence
- `random()`
	- Returns a random float between 0 and 1
- `seed(<int>)`
	- Given an integer seed, every time `random.random()` is called, it will behave as `random()` normally would, but will always generate floats in the same order, in a deterministic fashion
		- Thus, reliable encryption should not use this
## `requests` Module
- !!!
## `tempfile` Module
- !!!
## `threading` Module
- !!!
## `time` Module
- !!!
## `timeit` Module
- !!!
## `traceback` Module
- !!!
## `typing` Module
### `Any` (Colour)
### Classes
#### `Protocol` Class
- !!!!
## `typing_extensions` Module
### Decorators
- `override`
	- !!!
## `unittest` Module
- [[Projects (Python)#`unittest` Module|Here]]
# Cryptography
## cryptography
- !!!
## PyCryptodome
- !!!
# Debugging
## `ipdb` Module
- [[Projects (Python)#`ipdb` Debugger|Here]]
# Discord
## `discord.py` Library
### Introduction
#### Event Handler
- Upon `Client.connect()`, which creates a WebSocket connection to Discord, the event handler is also constructed
- When an event occurs, the WebSocket passes the data as an event to `Client.dispatch()`, which will either call the appropriate event handler or do nothing, depending on what is implemented
### Classes
#### `Client` Class
- !!! event
##### Methods
- `async close()`
	- Closes connection to Discord
- `async connect()`
	- Creates a websocket connection and lets it listen to messages from Discord
	- It is the coroutine that drives the event loop of the client
- `async fetch_guild(guild_id: int)`
- `async login(token: str)`
	- Logs into client with token and calls `setup_hook()`
- `async on_error(<event>)`
	- The default error handler of the client
	- By default logs to the library logger on error but can be overwritten to have a customized error handling
- `async setup_hook()`
	- Only fires once in the lifecycle of the bot
	- Thus, it is best to put set up here
- `async start(<token>: str)`
	- Shorthand for `login()` and `connect()`
- `async wait_for(<event>)`
	- Wait for a WebSocket event
- `async wait_until_ready()`
	- Wait until client's internal cache is ready to prevent race conditions
##### Decorators
- `@event`
	- Registers a, most likely, custom implementation of an [[#`discord.py` Library#Events|event]] for `discord.py` to listen to, so that when the event happens later, the custom implementation will execute
	- ```python
	  @client.event
	  async def on_ready():
		  print("Ready!")
	  ```
	- Sources
		- [StackOverflow](https://stackoverflow.com/questions/52689954/what-it-really-is-client-event-discord-py)
#### `Guild` Class
##### Attributes
- !!!
##### Methods
- `async fetch_channels() -> Sequence[abc.GuildChannel]`
	- Returns all channels in the guild
- `async for ... in fetch_members()`
	- Retrieves an asychronous iterator that enables receiving members
#### `Intents` Class
##### Attributes
- `members`
- `message_content`
- `presences`
##### Methods
- `default()`
	- Enables everything except certain intents:
		- `members`
		- `message_content`
		- `presences`
#### `Member` Class
##### Attributes
- `id`
- `name`
### Events
- Technically event handlers
- `on_connect()`
	- Literally the moment we've established a WebSocket connection with Discord
	- This is not to be confused with `on_ready()`, which is a little higher-level
- `on_disconnect()`
	- !!!
- `on_error()`
	- !!!
- `on_ready()`
	- !!!
# Input & Output
## `aiofiles` Library
- Sources
	- [OneUptime](https://oneuptime.com/blog/post/2026-02-03-python-aiofiles-async-files/view)
### Introduction
- All functions in `aiofiles` operate as coroutines
### Functions
- `flush()`
- `open()`
	- Context manager
	- Used to open files
	- Operates similarly to `open()` in [[#`builtins` Module|builtins]]
- `read()`
	- Like the native `read()`, reads up to size chars or bytes depending on the mode
	- By default, reads entire file
- `readall()`
	- !!!
- `readlines()`
	- Reads entire file and outputs list of strings by lines read
- `write()`
	- Like the native `write()`, writes data to file
- `writelines()`
	- Writes any iterable of strings to file
### Usage
- ```python
  import asyncio
  import aiofiles
  
  from pathlib import Path
  
  async def writeHelloWorldToFile(target_file: Path) -> None:
	  async with aiofiles.open(target_file, mode = 'w') as file:
		  await file.write("Hello world.")
  
  async def main() -> None:
	  await asyncio.create_task(writeHelloWorldToFile(Path("test.txt")))
  
  if __name__ == "__main__":
	  asyncio.run(main())
  ```
# Mathematics
## NumPy
- `numpy`
### Install
- !!!
## SageMath
### Install
- Mac
	- Console version
		- `brew install --cask sage`
## SymPy
- !!!
# Pwn
## pwntools
- `from pwn`
### Functions
- !!!
# Testing
## `pytest` Module
- [[Projects (Python)#pyTest|Here]]
## `pytest-asyncio` Module
- [[Projects (Python)#pyTest-asyncio|Here]]
## `pytest-mock` Module
- [[Projects (Python)#pyTest-Mock|Here]]
## `unittest` Module
- [[Projects (Python)#`unittest` Module|Here]]
