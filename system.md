# Operating System

- [Operating System](#operating-system)
    - [Memory leak](#memory-leak)
    - [Connection pool Timeout](#connection-pool-timeout)
    - [Thread Exhausion](#thread-exhausion)
    - [How do you know if you can handle 1K requests/s ?](#how-do-you-know-if-you-can-handle-1k-requestss-)
    - [Differences between process and thread?](#differences-between-process-and-thread)
    - [Garbage Collection](#garbage-collection)
    - [Stack and Heap](#stack-and-heap)
    - [How to communicate between threads and Processes?](#how-to-communicate-between-threads-and-processes)


### Memory leak  
1. Graph (CPU usage) increase by time. What cause this and how to solve?

    answer: Maybe a memory leak problem. 

    **Memory leak**: 
    >a memory leak is a type of resource leak that occurs when a computer program incorrectly manages memory allocations in a way that memory which is no longer needed is not released. 

    **Symptoms**: Works fast at first, but slower over time. `OutofMemoryError` after running. Sometimes crasges the applications.

    **Causes**: 
    - memory leak through static fields
    - Through unclosed Resources, a running server that lasts weeks or months.
    - Inproper equals and hashcode implementation.

    **Handle**:  
    - Enable profiling. Use tools to see how much memory used in part of your applications. Helps to identify the problem. 
    - Verbose Garbage Collection. Enable verbose garbage collection to track detailed trace of GC.
    - Get Error and Warning informations whenever it encounters obvious cases of memory leakage.
    - Code review.

### Connection pool Timeout
**Connection pool**: 
>a connection pool is a cache of database connections maintained so that the connections can be reused when future requests to the database are required.

**Meaning**: This value indicates the number of seconds that a connection request waits when there are no connections available in the free pool and no new connections can be created.

**Handle**: 
- Check connection pool configurations and logs about connection messages. 
- Check code for correct useage and releasing.

### Thread Exhausion
**Thread pool**:
> a thread pool is a software design pattern for achieving concurrency of execution in a computer program

**Thread exhausion** arises when generating more tasks than thread pool can handle. 

**Solve**: Use Asynchronous code with fewer threads to avoid blocking and threads.


### How do you know if you can handle 1K requests/s ?
Load test with mocked production data.


### Differences between process and thread?  
Both processes and threads are independent sequences of excution.

* Threads run in a shared memory space, while processes run in separate memory spaces.
* Each process provides the resources needed to execute a program. Each process is started with a single thread, often called the primary thread, but can create additional threads from any of its threads.
* A thread is an entity within a process that can be scheduled for execution.


### Garbage Collection
**what**:  
Once an object is **no longer referenced** and therefore is not reachable by the application code, the garbage collector removes it and reclaims the unused memory.

**Automatic GC**:  
Automatically handle the deletion of unused objects or inaccessible objects free up memory resources.  
Traditional way, programmers need to GC by themselves.

Senarios that not suitable for GC:  
Online service which need **low latency** and keep communication with users.(no "stop the world" time interval)


### Stack and Heap
Heap memory is used by all the parts of the application whereas stack memory is used only by one thread of execution. When an object is created, it's mostly stored in the Heap space and stack memory contains the reference to it.


### How to communicate between threads and Processes?
**Threads**:
- Thread communicate via shared memory. 

**Processes**:  
[details](https://www.usna.edu/Users/cs/wcbrown/courses/IC221/classes/L13/Class.html)  
Different processes in the same machine use IPC(inter process communication)
- Signals and Files
- FIFOs: named pipes, Stream of byte. Write and Read in FIFO way. 
    - if nothing to read, sleep the reading process
    - if buffer is full, sleep the writing process

- Pipes: using `|` in Linux. Like FIFOs without name. Pipe is **One-way**.

- Message queue, semaphore, shared memory, etc

