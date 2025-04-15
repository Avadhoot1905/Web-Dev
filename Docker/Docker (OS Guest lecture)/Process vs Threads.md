# What is a process?

- everything that runs on ur computer is a process
- program in execution
- piece of code = set of instructions for the computer = program

#funny : os signals
common signals:
- -s
- -l
- -signal_name
- -signal_number

also signals:
kill command: instant shutdown of application
sig command: graceful shutdown of application

#funny : file descriptor
ulimit: helps count the number of file descriptors that are open
# What is a thread?

- a single processing unit of a processor (might be wrong)
- single sequential activity in process
- parallelism, concurrency
- "light weight process"
## thread v subprocesses
- threads are more efficient
- subprocesses are bad at communication

## Why threads?
- better efficiency and output
- they have a "shared state"

## Multithread
- uses all cores efficiently
- each thread gets divided according to the number of cores
- very hard to write multithread

`java multithreading is different from python multithreading`

#funny 
- GIL - global interpreter lock 
	cpython has a lock for its internal shared global state
	makes multithread easier
	#imp

`python is not recommended in places where math heavy tasks are to be used and where all cpus need to be used effectively`

imp concepts from cat 2 
	- race condition
	- critical section
	- detecting deadlock
	#imp

`python multiprocesses helps us use all cores effectively`

different processes never interact unless ur doing smtg like ML
