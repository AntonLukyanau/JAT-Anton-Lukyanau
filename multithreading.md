## What is "thread safety"?
Thread safety is a property of an object or code that ensures that when executed or used by multiple threads, the code will behave as it is intended. For example, a thread-safe counter will not skip any count, even if the same counter instance is used by multiple threads.
## What is "cooperative multitasking"? What type of multitasking does Java use? What is the reason for this choice?
Cooperative multitasking is a way of dividing CPU time between threads, in which each thread is required to give control to the next one voluntarily.

The advantages of this approach are ease of implementation, lower overhead for context switching.

Disadvantages - if one thread hangs or behaves incorrectly, then the whole system hangs and other threads will never get control.

Java uses preemptive multitasking, in which the decision to switch between threads in a process is made by the operating system.

Unlike cooperative multitasking, control is transferred to the operating system regardless of the state of running applications, due to which, individual hung process threads, as a rule, do not "suspend" the entire system. Switching between tasks regularly also improves the responsiveness of the application and increases the speed of releasing resources that are no longer in use.

In implementation, preemptive multitasking differs from cooperative multitasking, in particular, in that it requires the processing of a system interrupt from a hardware timer.
## How is a process different from a thread?
A process is an instance of a program at runtime, an independent entity that is allocated system resources (such as CPU time and memory). Each process runs in a separate address space: one process cannot access the variables and data structures of another. If a process wants to access other people's resources, it must use inter-process communication. These can be pipelines, files, communication channels between computers, and much more.

For each process, the OS creates a so-called "virtual address space" to which the process has direct access. This space belongs to the process, contains only its data and is at its complete disposal. The operating system, on the other hand, is responsible for how the process's virtual space is mapped onto physical memory.

Thread (thread) - a specific way of executing a process, which determines the sequence of code execution in the process. Threads are always created in the context of a process, and their entire life passes only within its boundaries. Threads can execute the same code and manipulate the same data, and share handles to kernel objects, because the handle table is not created in separate threads, but in processes. Since threads use significantly less resources than processes, it is more beneficial to create additional threads while doing work and avoid creating new processes.
## What are "green threads" and do they exist in Java?
Green (lightweight) threads (green threads) - threads emulated by a virtual machine or runtime environment. Creating a green thread does not imply creating a real OS thread.

The Java Virtual Machine takes care of switching between different green threads, and the machine itself runs as a single OS thread. This provides several benefits. OS threads are relatively expensive on most POSIX systems. Also, switching between native threads is much slower than switching between green threads.

This all means that in some situations green threads are much more profitable than native threads. A system can support many more green threads than OS threads. For example, it's much more practical to start a new green thread on a new HTTP connection to a web server, rather than creating a new native thread.

However, there are also disadvantages. The biggest one is that you can't run two threads at the same time. Since there is only one native thread, it is the only one called by the OS scheduler. Even if you have multiple processors and multiple green threads, only one processor can call a green thread. And all because from the point of view of the OS task scheduler, all this looks like one thread.

Since version 1.2, Java has supported native threads, and since then they have been used by default.
## How can you create a thread?
Create a child of the Thread class and override its run() method;
Create an object of the Thread class by passing it an instance of the class that implements the Runnable interface in the constructor. This interface contains a run() method that will be executed on a new thread. The thread will finish executing when its run() method completes.
Call the submit() method on an instance of a class that implements the ExecutorService interface, passing it an instance of a class that implements the Runnable or Callable interface as a parameter (it contains the call() method, which describes the execution logic).
## What is the difference between Thread and Runnable?
Thread is a class, some superstructure on a physical thread.

Runnable is an interface that represents an abstraction over a running task.

In addition to helping to solve the problem of multiple inheritance, Runnable is a clear advantage of using it is that it allows you to logically separate the execution logic of the task from direct flow control.
## What is the difference between the start() and run() methods?
Even though start() calls the run() method internally, it's not the same as just calling run() . If run() is called like a normal method, then it is called on the same thread and no new thread is started, as is the case when you call the start() method.
## What is a "monitor" in Java?
Monitor, mutex (mutex) is a means of providing control over access to a resource. A monitor can have a maximum of one owner at any given time. Therefore, if someone is using a resource and has seized a monitor for sole access, then another who wants to use the same resource must wait for the monitor to be released, seize it, and only then start using the resource.

It is convenient to think of a monitor as the id of the object that captured it. If this id is equal to 0, the resource is free. If not 0, the resource is busy. You can stand in line and wait for him to be released.

In Java, each object instance has a monitor that is controlled directly by the virtual machine. It is used like this: any non-static synchronized method, when it is called, first of all tries to capture the monitor of the object on which it is called (which it can refer to as this). If it succeeds, the method is executed. If not, the thread stops and waits for the monitor to be released.
## Define the term "synchronization".
Synchronization is a process that allows threads to execute in parallel.

In Java, all objects have a single lock, which means that only one thread at a time can access the critical code in the object. This synchronization helps prevent object state corruption. Once a thread has acquired the lock, no other thread can enter the synchronized code until the lock is released. When the thread holding the lock exits the synchronized code, the lock is released. Now another thread can acquire the object's lock and execute the synchronized code. If a thread attempts to acquire a lock on an object while another thread owns the lock, the thread enters the Locked state until the lock is released.
## What are the ways to synchronize in Java?
System synchronization using wait()/notify(). A thread that is waiting for some conditions to be met calls the wait() method on this object, having previously captured its monitor. This stops his work. Another thread can call the notify() method on the same object (again, having previously captured the object's monitor), as a result of which the thread waiting on the object “wakes up” and continues its execution. In both cases, the monitor must be captured explicitly, through a synchronized block, because the wait () / notify () methods are not synchronized!

System synchronization using join(). The join() method, called on an instance of the Thread class, allows the current thread to stop before the thread associated with that instance has finished running.

Using classes from the java.util.concurrent package, which provides a set of classes for organizing inter-thread communication. Examples of such classes are Lock, Semaphore, etc. The concept of this approach is to use atomic operations and variables.
## What states can a thread be in?
Threads can be in one of the following states:

New (New). Once a thread is instantiated, it is in the New state until the start() method is called. In this state, the thread is not considered alive.
Runnable. The thread enters the Runnable state when the start() method is called. A thread can also enter this state from the Running state or from the Blocked state. When a thread is in this state, it is considered alive.
Working (Running). A thread transitions from the Runnable state to the Running state when the Thread Scheduler selects it as currently running.
Alive, but not runnable. A thread can be alive but not running for several reasons:
Waiting The thread enters the Wait state by calling the wait() method. Calling notify() or notifyAll() can bring the thread from the Idle state to the Runnable state.
Sleeping. The sleep() method puts the thread into the Sleep state for the specified amount of time in milliseconds.
Blocking (Blocked). A thread may enter this state while waiting for a resource, such as I/O, or because another object is blocking. In this case, the thread transitions to the Runnable state when the resource becomes available.
Dead (Dead). A thread is considered dead when its run() method is fully executed. A dead thread cannot transition to any other state, even if the start() method is called on it.
## How do the wait() and notify()/notifyAll() methods work?
These methods are defined in the Object class and are intended for the interaction of threads with each other during inter-thread synchronization.

wait(): releases the monitor and puts the calling thread into a wait state until another thread calls the notify()/notifyAll() method;
notify(): continues the work of a thread that had previously called the wait() method;
notifyAll(): Resumes all threads that have previously had their wait() method called.
When the wait() method is called, the thread releases the lock on the object and transitions from the Running state to the Waiting state. The notify() method signals one of the threads waiting on the object to enter the Runnable state. In this case, it is impossible to determine which of the waiting threads should become operational. The notifyAll() method causes all waiting threads for the object to return to the Runnable state. If no thread is waiting on the wait() method, then nothing happens when notify() or notifyAll() is called.

A thread can call the wait() or notify() methods on a particular object only if it currently has a lock on that object. wait(), notify(), and notifyAll() should only be called from synchronized code.
## How does the wait() method work with and without a parameter?
wait()

without parameters, releases the monitor and puts the calling thread into a waiting state until another thread calls the notify()/notifyAll() method,
with parameters will cause the thread to wait the specified amount of time or a call to notify()/notifyAll().
## How are Thread.sleep() and Thread.yield() methods different?
The yield() method causes the thread to transition from the running state to the runnable state, allowing other threads to become active. But the next thread selected to run may not be different.

The sleep() method causes the current thread to sleep for the specified time, the state changes from running to waiting.
## What is a deadlock?
Deadlock is a phenomenon in which all threads are in a waiting mode. Occurs when the following states are reached:

Mutual Exclusion: At least one resource is occupied in undivided mode and therefore only one thread can use the resource at any given time.
holds and waits: A thread holds at least one resource and requests additional resources held by other threads.
no preflushing: the operating system does not reassign resources: if they are already busy, they must be given to holding threads immediately.
circular waiting: a thread is waiting for a resource to be released by another thread, which in turn is waiting for a resource locked by the first thread to be released.
The simplest way to avoid deadlock is to avoid looping. This can be achieved by acquiring shared resource monitors in a specific order and freeing them in reverse order.
## What is livelock?
livelock is a type of deadlock in which multiple threads perform useless work, getting into a loop while trying to acquire any resources. At the same time, their states are constantly changing depending on each other. No actual error occurs, but system efficiency drops to 0. Often occurs as a result of attempts to prevent a deadlock.

A real-life example of livelock is when two people meet in a narrow corridor and each, trying to be polite, steps aside, and so they endlessly move from side to side, absolutely not moving in the direction they need.
## How to check if a thread is holding the monitor of a particular resource?
The Thread.holdsLock(lock) method returns true when the current thread holds the monitor on the specified object.
## What is the volatile, synchronized, transient, native keyword used for?
volatile - This modifier forces threads to turn off access optimization and use a single instance of the variable. If the variable is of a primitive type, this will be enough to ensure thread safety. If the variable is a reference to an object, only the value of this reference will be synchronized. However, the data contained in the object will not be synchronized!

synchronized - this reserved word allows you to achieve synchronization in methods or blocks of code marked with it.

The transient and native keywords have nothing to do with multithreading, the first is used to indicate class fields that do not need to be serialized, and the second signals that the method is implemented in platform-specific code.
## What is the difference between volatile and atomic variables?
volatile enforces a single instance of the variable, but does not guarantee atomicity. For example, the operation count++ will not become atomic simply because count is declared volatile. On the other hand, class AtomicInteger provides an atomic method to perform such complex operations atomically, for example getAndIncrement() is an atomic replacement for the increment operator, it can be used to atomically increment the current value by one. Atomic versions are constructed similarly for other data types.
## What are daemon threads?
Daemon threads run in the background with the program, but are not an integral part of the program. If a process can run in the background of the main threads of execution and its activity is to serve the main threads of the application, then such a process can be started as a daemon thread using the setDaemon(boolean value) method called on the thread before it starts. The boolean isDaemon() method allows you to determine whether the specified thread is a daemon or not. The basic property of daemon threads is that the main application thread can terminate the daemon thread (unlike normal threads) at the end of the main() method code, regardless of the fact that the daemon thread is still running.
## Is it possible to make the main thread of a program a daemon?
No. Daemon threads allow you to describe background processes that are needed only to service the main threads of execution and cannot exist without them.
## What is a race condition?
A race condition is a design error in a multi-threaded system or application, in which this work directly depends on the order in which the threads are executed. A race condition occurs when the thread that should execute first loses the race and another thread runs first: the behavior of the code changes, causing non-deterministic errors.
## Is there a way to solve the race condition problem?
Common solutions:

Using a local copy is copying a shared variable into a thread local variable. This method works only when there is only one variable and copying is done atomically (in one machine instruction), using volatile.
Synchronization - operations on a shared resource occur in a synchronized block (using the synchronized keyword).
Combining Methods - The above methods can be combined by copying "dangerous" variables in a synchronized block. On the one hand, this removes the restriction on atomicity, on the other hand, it allows you to get rid of too large synchronized blocks.
There are no obvious ways to detect and fix race conditions. The best way to get rid of races is to properly design a multitasking system.
## Why is it not recommended to use the Thread.stop() method?
When forcibly stopping (suspending) a thread, stop() interrupts the thread at a non-deterministic execution location, as a result it becomes completely unclear what to do with the resources that belong to it. A thread may open a network connection - in this case, what to do with the data that has not yet been read out? Where is the guarantee that after further launch of the thread (in case of suspension) it will be able to read them up? If a thread has locked a shared resource, then how to release this lock and won't forced release lead to system consistency violation? The same can be extended to the case of a database connection: if the thread is stopped in the middle of a transaction, then who will close it? Who and how will unlock resources?

