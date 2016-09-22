# Operating System

## What is a thread?
In most cases a thread is a component of a process. Multiple threads can exist within one process, executing concurrently and sharing resources such as memory, while different processes do not share these resources. 


Systems with a single processor generally implement multithreading by time slicing: the central processing unit (CPU) switches between different software threads. This context switching generally happens very often and rapidly enough that users perceive the threads or tasks as running in parallel. On a multiprocessor or multi-core system, multiple threads can execute in parallel, with every processor or core executing a separate thread simultaneously; on a processor or core with hardware threads, separate software threads can also be executed concurrently by separate hardware threads.

## What is a process?
In computing, a process is an instance of a computer program that is being executed. It contains the program code and its current activity. Depending on the operating system (OS), a process may be made up of multiple threads of execution that execute instructions concurrently.

## Process vs Threads

Fault-tolerance and scalability is the main advantages of using processes vs. threads.


A system that relies on shared memory or some other kind of technology only available when using threads, will be useless you want to run the system on multiple machines. Sooner or later you need to communicate between different processes.


Using processes you are forced to deal with communication through messages, which is the Erlang way of doing communication. Data is not shared, so there is no risk of data corruption.


Another advantage of processes is that they can crash and you are perfectly ok with that, because you just restart them (even across network hosts). If thread crashes, it may crash the entire process, which may bring down your entire application. If an Erlang process crashes, you will only lose that phone call, or that webrequest, etc.


OS processes have many drawbacks that make them harder to use, like the fact that it takes forever to spawn a new process. However, Erlang has it's own notion of processes, which are extremely lightweight.


With that said, this discussion is really the topic of research. Please read Joe Armstrongs paper on fault-tolerant systems if you want to know more about Erlang and this kind of philosophy.


##### Summary: 

Pros of using processes:
- Better for fault-tolerance and scalability
- No risk of data corruption
- Threads are useless when running the system on multiple machines
- Can handle a crash ("simple" restart)


Cons of using Processes:
- Harder to use
- Takes a while to start a new process


Cons of using Threads:
- if it crashes, can crash the process then the application


## What is concurrency?
Concurrency is the decomposability property of a program, algorithm, or problem into order-independent or partially-ordered components or units.[1] This means that even if the concurrent units of the program, algorithm, or problem are executed out-of-order or in partial order, the final outcome will remain the same. This allows for parallel execution of the concurrent units, which can significantly improve overall speed of the execution in multi-processor and multi-core systems.



## Concurrency Issues
- Race condition: which basically is assuming that one piece of code will run before / after another concurrent piece of code.
- deadlocks: that is code A waits for code B to release resource Y, while code B is waiting for A to release resource X.

## What's the difference between deadlock and livelock?

### Definition #1


Deadlock:

A situation in which two or more processes continuously change their states in response to changes in the other process(es) without doing any useful work.

Livelock:

A situation in which two or more processes continuously change their states in response to changes in the other process(es) without doing any useful work.



### Definition #2


A livelock is similar to a deadlock, except that the states of the processes involved in the livelock constantly change with regard to one another, none progressing. Livelock is a special case of resource starvation; the general definition only states that a specific process is not progressing.


Example of Livelock:

A real-world example of livelock occurs when two people meet in a narrow corridor, and each tries to be polite by moving aside to let the other pass, but they end up swaying from side to side without making any progress because they both repeatedly move the same way at the same time.


Deadlock is a condition in which a task waits indefinitely for conditions that can never be satisfied - task claims exclusive control over shared resources - task holds resources while waiting for other resources to be released - tasks cannot be forced to relinguish resources - a circular waiting condition exists.



## Avoiding Deadlock and livelocks
1. Keep an eye on the context when your declare a variable
2. Lock the access to mutable class or instance attributes: Variables that are part of the same invariant should be protected by the same lock.
3. Avoid Double Checked Locking
4. Keep locks when you run a distributed operation (call subroutines).
5. Avoid busy waiting
6. Keep the workload low in synchronized sections
7. Do not allow to take a client control while you are in a synchronized block.
8. Comments! This really helps to understand what the other guy had in mind with declaring this section synchronized or that variable immutable


## What is Double Check locking?
Double check locking is a software design pattern used to reduce the overhead of acquiring a lock by first testing the locking criterion (the "lock hint") without actually acquiring the lock. The pattern, when implemented in some language/hardware combinations, can be unsafe. At times, it can be considered an anti-pattern.


http://erlang.org/download/armstrong_thesis_2003.pdf
http://stackoverflow.com/questions/4315292/concurrency-processes-vs-threads
https://en.wikipedia.org/wiki/Thread_(computing)
https://en.wikipedia.org/wiki/Concurrency_(computer_science)
http://stackoverflow.com/questions/520837/what-are-common-concurrency-pitfalls
http://stackoverflow.com/questions/6155951/whats-the-difference-between-deadlock-and-livelock
https://www.quora.com/What-is-the-difference-between-deadlock-and-livelock-deadlock-infinite-recursion-and-starvation