# Asynchronous and Threading :material-pirate:

!!! note
    This is not part of the Syllabus but is important in modern computing. 

Devices like the Arduino Uno have a single central processing unit (CPU) or core. This was the same for the majority of computers up until about 2001 for commercial computing and 2005 for personal computers when the duel core Pentium processor was released. Since then more cores have been added and these days you home PC could have up to 24 cores and 32 threads. Also note, that threads for a CPU are different from software threading. Your mobile phone will have up to 8 cores in it. 

What does all this mean? `¯\_(ツ)_/¯`

## Asynchronous 
Is the ability for a single thread or process to pause what it is doing to give CPU time back to other processes that might need it. This is typically used in processes that can take a long time to complete like a request sent over the Internet, reading a file or a query on a database to name a few.

Consider someone who needs to call a service like an airline. When they make the call they get put in a queue waiting for someone to answer. This is a synchronous task as you cannot really do anything while you are waiting for the person on the other end to answer the call. If however, they offer a callback service so that when a customer representative is available the will call you, this is asynchronous as you can hang up the phone and go about doing other things until the call you back.

``` mermaid
sequenceDiagram
    autonumber
    actor User
    User->>WebForm: Enter your details
    User->>WebForm: Press Submit
    WebForm->>+Database: Async(Process Request)
    WebForm->>User: Show spinning wheel
    Database-->>-WebForm: Success
    WebForm->>User: Update Display
```

## Further Information


## Threading
Is the ability for there to be multiple processes running at the same time. This is possible on a single core machine but requires logic in the operating system to interrupt each process storing the state of the process to allow another process to run. When you have multiple cores then each thread can run on a separate core to speed up the compute time.

Consider you are working on a group project. When you get the project you break it up into multiple parts so that each of you can work on it separately. Each person is acting as a separate thread of work doing their own processing. So, maybe someone does the drawings, another does the text and the third sources the materials for the poster. When you combine your work on the poster this is the same as the threads finishing and the results being collected.

``` mermaid
sequenceDiagram
    actor Client1
    actor Client2
    par Client1 to Server
        Client1->>Server: Request some data
        Server-->>Client1: Response
    and Client2 to Server
        Client2->>Server: Request other data
        Server-->>Client2: Response
    end
```

## Further Information