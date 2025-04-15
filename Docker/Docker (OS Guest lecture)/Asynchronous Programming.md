
- all issues of multithreading are solved using async

async.io 
	- python library for async
	- its like a whole different lang

- async wait helps in getting data to frontend from backend
- handled at os level
- imagine ur reading a file and the os changes to another thread, u would get a different output, the context switch would cause havoc
- adv: u get to choose when to context switch #imp
- yield and awake keywords in python

# CPU bound V IO Bound


- If the operation is CPU bound, use multiprocessing and parallelism
- If the operation is IO Bound, use threading or coroutines #imp 