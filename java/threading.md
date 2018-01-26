# What is threading?

Series of instructions that can be performed till it's interrupted. Or it's finished executing.

# Threading vs processes?

When an application component starts and the application does not have any other components running, the Android system starts a new Linux process for the application with a single thread of execution. By default, all components of the same application run in the same process and thread (called the "main" thread). It just uses if the same process and thread if that application already exists with a different component.


In short, all application components run in a single process. One (main) thread starts on startup but you can start more to perform background.


# Example of creating a new thread

```
Thread t = new Thread(new Runnable() {
    public void run() {
        /*
         * Do something
         */
    }
});

t.start();
```

# Stopping a thread

Internally

```
if (Thread.currentThread().isInterrupted()) {
```

Externally

```
t.stop();
```


Source:
- https://codereview.stackexchange.com/questions/56428/run-different-methods-in-background-threads-without-duplication
- https://developer.android.com/guide/components/processes-and-threads.html
- https://www.quora.com/What-is-threading-in-programming-terms
