# Concurrency != Parallelism

- Parallelism = doing more than one thing at the same time (multiple cores)
  - real parallel execution of tasks
- Concurrency = providing illusion of doing more than one thing at the same time (only one core)
  - switching constantly between tasks

## Interprocess communication

1. Files
   - multiple processes uses one file to share data i.e. user.tmp
2. SIGNAL
   - SIGNAL like SIGKILL
3. Pipes
   - ls | grep 'hello' 
   - stdin -> command/process -> stdout | stdin -> command/process -> stdout
4. Sockets
   - client process communicates with server process via sockets
     - network sockets for remote calls
     - UNIX domain sockets (limited to same machine)
   - localhost:8080

## Threads
- one process but multiple threads 
- for instance 1 thread for garbage collection, 1 thread for code execution etc.
- multiple CPUs can execute multiple threads at the same time

### Stack and Heap
- Stack 
  - local variables, method parameters
  - endless recursive method call -> StackOverFlow
- Heap
  - holds process parameters
  - stores objects/data shared between threads

### Thread Contention
- Race conditions when >1 threads write to shared resources (i.e. lists)
- using Locks or other Mutex mechanism
- thread competition, so not too many threads (balance it out)

### Thread Pools
- limit of threads
- until limit is not reached, a new thread is created