# Operating System

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


http://erlang.org/download/armstrong_thesis_2003.pdf
http://stackoverflow.com/questions/4315292/concurrency-processes-vs-threads