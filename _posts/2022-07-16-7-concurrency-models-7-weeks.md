---
anchor_id: 7 weeks
title: Seven Concurrency Models in Seven Weeks
layout: blog_post
---

Last year, I read the excellent and very interesting [Seven Concurrency Models in Seven Weeks](https://pragprog.com/titles/pb7con/seven-concurrency-models-in-seven-weeks/) (though in somewhat more than seven weeks). This is a very long post with my notes from reading it.

## TL;DR: you can follow along with the book using my Vagrantfile

I created a [Vagrantfile](https://github.com/annashipman/7weeks-concurrency) to run the code samples in. You can use this to follow along with the book.

There are a couple of places where the code has to be changed in order to run but I have left that as an exercise to the reader; the error messages tell you enough.

There are some examples (e.g. Hadoop) that won't work on the Vagrant box.

## There is a difference between concurrent and parallel

Concurrent and parallel are different but related concepts. A concurrent program has multiple logical threads of control. A parallel program is executing different parts of the computation simultaneously, and may or may not have more than one logical thread of control.

<div class="code-sample">
<p>Let's say we are tidying the house.</p>
<p>Concurrency: I do the washing up while you hoover the house.</p>
<p>Parallelism: I hoover downstairs and you hoover upstairs at the same time.</p>
</div>

Another way of thinking about it is that concurrency is an aspect of the problem domain: your program needs to handle multiple simultaneous events. Parallelism is an aspect of the solution domain; you want to make your program faster by processing different parts of the problem in parallel.

## Week One: Threads and Locks

The "first week" is about threads-and-locks programming. This is a really great intro to concurrency because it is very low-level; "little more than a formalization of what the underlying hardware actually does", so it helps you to get a foundational understanding of what's going on.

I've included more notes on this as some of the key themes of concurrent programming are included in this section.

The book points the reader towards the [FAQ for JSR 133](http://www.cs.umd.edu/~pugh/java/memoryModel/jsr-133-faq.html). A JSR is a Java Specification Request, and JSR 133 updates the original Java Memory Model. It explains what a memory model does at the processor level, and explains important ideas, like for example the fact that a compiler might move a write operation earlier or later than it appears in the written program, to improve performance.

Java includes language constructs like `volatile` and `synchronized`, which are intended to help the programmer describe a program's concurrency requirements to the compiler. However, you have to make sure you are using them correctly and it's very easy to incorrectly synchronise your program so it is not threadsafe.

### Intrinsic locks

Every Java object has an intrinsic lock. However, there are problems with the intrinsic locks. For example, you can't interrupt a thread that is blocked trying to acquire a lock – the only way to do this is to kill the JVM. So Java introduced other locking techniques, for example `ReentrantLock` which allows interruptible locks and timeouts. Though this is still not a perfect solution; for example it can lead to `livelock` where all the threads time out at the same time and become deadlocked again.

The book then talks through some other locking mechanisms, for example hand-over-hand locking (where you lock a small portion, e.g. of a linked list), fairness parameter on `ReentrantLock` (the lock obeys the order of the lock request) and `Condition` variables (allow you to wait on the thing you need. The thread acquires the lock and checks to see if the thing is ready. If it's not, it releases the lock and waits again).

### Atomic variables are an alternative to locks

Another option instead of intrinsic locks is atomic variables, for example `AtomicInteger` counter will read a value and increment atomically. This is better than using a lock because you can't forget to acquire the lock; and also it's impossible for it to deadlock.

Atomic variables are the foundation of non-blocking, lock-free code.

### Don't roll your own locking solution

While it's important to understand how locks work, it's better to use concurrent data structures rather than roll your own locking solution. For example, if you create a thread for each incoming connection, you might run out of processors, and it's a perfect attack vector for a DoS. Better is to create a thread pool of a certain size (e.g. approximately same number of threads as processors for computation intensive tasks, or perhaps twice as many threads as processers for IO-intensive tasks). If more requests are active, they will be queued until a thread becomes free; so we won't grind to a halt – and we also won't incur the cost of starting a new thread for each request.

### An example

Throughout the book, we return to the same example of how we might speed something up by parallelising. The example is counting words in an XML dump of Wikipedia, using the producer-consumer pattern. The producer produces the pages from the XML dump. The consumer consumes those pages and counts the words.

The producer is very quick. So to speed things up, we could parallelise the consumer. However, if we are going to do that, we need to find a way to synchronize access to the counts map.

We could lock within each count. But what that does is mean that each consumer spends more time waiting for the map to be unlocked than they do actually do doing work (excessive contention).

We can use `ConcurrentHashMap`, which provides atomic read-modify-write methods, and has also been designed to support high levels of concurrent access via a technique called lock-striping. We can speed it up even further by batching the jobs, i.e. each consumer keeps a local word count and we merge them when we exit the program.


Instead of a thread pool you might use a `ForkJoinPool`, which works by 'work-stealing'; this means the threads actively look for tasks to execute in the pool. This makes for efficient processing when the majority of the other tasks spawn small sub-tasks, or many small tasks are submitted.

A `CyclicBarrier` is something that allows a set of threads to all wait for each other until they've all reached a common barrier point ('cyclic' means it can be reused). A `CountDownLatch` is another way of performing a similar action: in this case you set a count and once that number of threads has called the countDown() method it releases all waiting threads.

### There is a limit to how much speedup parallelising can give you

If you time the speedup you get from parallelising, what you see is: performance initially increases linearly. It is then followed by a period where it increases more slowly. Eventually it will peak and adding more threads will only make it slower.

[Amdahl's Law](https://en.wikipedia.org/wiki/Amdahl%27s_law) is a formula that gives the theoretical speedup that parallelising a program can give. It relates to how much of the program can be parallelised.

Long after I'd finished reading the book but before I'd finished this write-up, I attended a brilliant keynote at QCon on [the future of microprocessors](https://qconlondon.com/london2022/keynote/future-microprocessors) by [Sophie Wilson](https://royalsociety.org/people/sophie-wilson-12544/). In it she talked about Amdahl's law and noted that what most people miss about it is how aggressive it is.

![Graph showing theoretical speedup of a program as a function of number of processors](/img/AmdahlsLaw.svg)
By <a href="https://en.wikipedia.org/wiki/User:Daniels220" class="extiw" title="wikipedia:User:Daniels220">Daniels220</a> at <a href="https://en.wikipedia.org/wiki/" class="extiw" title="wikipedia:">English Wikipedia</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=6678551">Link</a>

The graph shows that where 95% of the program is parallelisable, you can get it up to 20 times faster. Where 90% is parallelisable, this drops to only 10 times faster. And if only 50% of the program is parallelisable, the most speedup you can get is only 2x.

### Strengths and weaknesses of threads-and-locks programming

The main strength of threads-and-locks programming is that it's little more than the hardware offers so can be very efficient when applied correctly.

However, you don't get much support on top of that; and it only supports shared-memory architectures, so can't be used to solve distributed problems. Threads-and-locks programming also doesn't provide direct support for parallelism, only concurrency.

But what makes it really hard is that it is impossible to test. Bugs tend to be intermittent and infrequent and may take a long time to show up, and there is no way to write automated tests that validate you've executed threading correctly. Because of that latter point, you can't reliably refactor the code.

## Week Two: Functional programming

Functional programming avoids many of the problems with threads-and-locks by avoiding mutable state.

An imperative program consists of a series of statements that change global state when executed. In contrast, a functional program models computation as the evaluation of expressions. These expressions are both first-class (i.e. can be manipulated like any other value) and do not have side effects. This lack of side effects makes reasoning about thread safety much easier. Immutable data dosn't need to be locked because multiple threads can't change it.

You can't always tell when you have mutable state. It might be hidden, e.g. in a function you are calling. He also gives an example of escaped mutable state, where it looks at first glance that everything is synchronised that should be, but one method returns an iterator, and the iterator still has access to the mutable state it is iterating on.

### Side note: My Vagrantfile wasn't working exactly as planned

While I could run the Java examples in my Vagrant box, the Clojure examples did not work as expected. I [wrote all that up in a separate post](/jfdi/clojure-vagrant.html); the summary is, I could not get these examples working correctly but learned a lot about Clojure in the process.

For example, sequences are lazy; as well as not evaluating later parts of a sequence until and unless we need them, it also discards the elements at the front if we've finished with them (we don't "hold on to our head"). This means if you run something like `take-last 5 (range 0 100000000)` might take a while to run but won't cause you to run out of memory.

This [Clojure cheatsheet](https://clojure.org/api/cheatsheet) is great.

### Functional programming allows us to parallelise code more easily because it is declarative

In imperative languages like Java, things happen roughly in the order you write them, leaving aside some moving around by the compiler and runtime.

In functional languages, it is declarative. Instead of writing a set of instructions for how to perform some operation, you give a statement of what the results should be, so there is more freedom to reorder calculations.

Pure functions are referentially transparent; this means that anywhere an invocation of the function appears, we can replace it with its result without changing the behaviour of the program. in fact one way to think about what executing functional code means is to think of it as repeatedly replacing function invocations with their results until you reach the final result. Because *every* function is referentially transparent, we can safely make changes to evaluation order, and thus we can easily parallelise.

The primary benefit of functional programming is confidence that your program does what you think it does. It can be difficult to get into the mindset but once you have, functional programs tend to be simpler, easier to reason about and easier to test than their imperative equivalents.

### Futures and promises

Dataflow programming is the idea that you push data towards functions that need them for their input. So you can execute the functions that do not have interdependencies concurrently, but some functions will need to wait for those to be executed before they can start.

Clojure allows us to use this execution strategy through futures and promises.

A future takes a body of code and executes it in another thread. The return value is a future object, and we get the value by dereferencing it using `deref` or `@`. This will block until the value is available.

A promise is very similar to a future, but creating a promise does not cause any code to be run. Instead its value is set with `deliver`.

A classic case for futures is talking to another web service. A future allows computation, such as network access, to take place on another thread while the main thread continues.

I loved the [summary of concurrency in Clojure at the start of this tutorial](https://ericnormand.me/guide/clojure-concurrency).

## Week Three: The Clojure Way (a.k.a. what about mutable state?!)

Some problems have modifying state as an inherent part of the solution. For this there is the "Clojure way"; the idea is that it uses functional programming *and* mutable state to get the best of both worlds.

A "pure" functional language provides no support for mutable data at all, so Clojure is "impure". It provides a number of different concurrency-aware mutable variables.

The difference between an impure functional language and an imperative language is emphasis. In an imperative language, variables are mutable by default and idiomatic code modifies them frequently. In an impure functional language, variables are immutable by default and idiomatic code modifies those that aren't only when absolutely necessary.

### Data structures are persistent

All of Clojure's data structures are persistent. This means that they always preserve the previous version when they are modified, so code can have a consistent view of the data in the face of modifications.

Persistent data structures separate identity from state. For example, a thread might have a reference to a data structure – the identity. The state may vary. This is different from an imperative language when a single identity has a single value, making it easy to lose sight of the fact that state is really a sequence of values over time. He quotes Heraclitus "You could not step twice into the same river; for other waters are ever flowing onto you".

### Supporting shared mutable state

To support shared mutable state in Clojure, you can use atoms, agents, or refs.

- Atoms. An atom is an atomic variable, very similar to Java's atomic variables – in fact Clojure atoms are built on `java.util.concurrent.atomic` An atom allows you to make independent, synchronous changes to a single value – synchronous because when `swap!` returns, the update has taken place
- Agents. Like atoms in that they encapsulate a reference to a single value which can be deferenced and is changed using `send`. However, `send` returns immediately, before the value of the agent has been changed, and the function passed to `send` is called some time later. Asynchronous updates have benefits, especially for long-running operations. But they also have added complexity.
- Refs are more sophisticated – providing [software transactional memory](https://en.wikipedia.org/wiki/Software_transactional_memory) (STM), which means we can make changes to to multiple variables; concurrently and in a co-ordinated fashion. However, they have to be changed as part of a transaction. Transactions are ACI (atomic, consistent and isolated) but not D (durable). As per database transactions. If you need durable; use a database instead.

How to choose between these approaches? To a certain extent it's a matter of personal preference, but even though STM gets the headlines, atoms suffice for most problems, as the language's functional nature leads to minimal use of mutable data. "As always, the simplest approach that will work is your friend".

## Week Four: Actors

Actors do away with shared mutable state altogether. Functional programming avoids the problems associated with shared mutable state by avoiding mutable state. Actor programming retains mutable state, but avoids sharing it.

An actor is a bit like an object in Object-Oriented programming. It encapsulates state and communicates with other actors by exchanging messages. The difference is actors run concurrently and they really do send messages (as opposed to OO where it's actually just calling a method).

For this chapter, the language used is Elixir (which runs on the Erlang JVM. Fun fact! Erlang uses [British spellings](https://github.com/elixir-lang/elixir/issues/9269), good reason to use it!).

In Elixir, an actor is called a process. In most environments, a process is a heavyweight entity that consumes a lot of resources and is expensive to create. In Elixir however, it's lightweight, lighter weight than most system threads, and Elixir programs typically create thousands of processes without problems. An actor is like a rental car. It's easy to get hold of, and you don't fix it if it breaks down, you just get another one.

You define an actor, the messages it knows how to receive and what it does when it receives them.

One of the most important features of actor programming is that messages are sent asynchronously, and placed in a mailbox. An actor handles messages sequentially, in the order they were added to the mailbox, moving onto the next message only when it's finished processing the current message.

A supervisor is a system process that monitors one or more worker processes and takes appropriate action if they fail. This can include restarting it. Actor programs tend to avoid defensive programming and instead let it crash, allowing the actor's supervisor to address the problem instead. This has multiple benefits, including:

- code is simpler and easier to understand, with a clear separation between 'happy path' and fault-tolerant code
- actors are separate from one another and don't share state, so there's little danger that a failure in one actor will adversely affect another
- As well as fixing the error, the supervisor can log it so we become aware of problems

One of the actor model's primary benefits is that it supports distribution. Sending a message to an actor on another machine is just as easy as sending it to one running locally.

There is a library called OTP which automates the creation of the underlying workers. (OTP is Open Telecom Platform as Erlang started out in telecommunications, but very little of it is now telecom-specific so it's now just "OTP").

In a way, actors are more object-oriented than OO objects, with stricter method-passing and encapsulation. Actors do not share state, and although they run concurrently with each other, within a single actor everything is sequential, which means we only need to worry about concurrency when considering message flows between actors. So actors can be tested in isolation, and if we find a concurrency bug we know it's in message flows.

Distributed programming means an actor program can scale to solve problems of almost any size, we are not limited to problems that fit on a single system. However, there is not direct support for parallelism. Parallel solutions need to be built from concurrent building blocks, raising the spectre of non-determinism.

## Week Five: Communicating Sequential Processes

Like functional programming and actors, CSP is an old idea that has experienced a renaissance, initially because of Go.

CSP is about focusing on the roads, rather than the cars. The features and capabilities of a message-passing systems are not primarily defined by the code between which messages are exchanged, or their content, but by the transport over which they travel.

In CSP channels are first class. Instead of each process being tightly coupled to a single mailbox, channels can be independently created, written to, read from and passed between processes.

A channel is a threadsafe queue. Any task with a reference to a channel can add messages to one end, and any task with a reference to it move messages from the other. Unlike actors, where messages are sent to and from specific actors, senders don't have to know about receivers or vice versa.

Treating the channels as first class gets rid of callback hell in two areas where there is traditionally a lot: asynchronous IO and UI programming.

One weakness of CSP is that there is not as much focus on distribution and fault tolerance. Also, as with both threads-and-locks and actors, CSP programs are susceptible to deadlock and have no direct support for parallelism.

Most of the difference between actors and CSP result from the differing focus of the communities: Actors has focused on fault tolerance and distribution and CSP on efficiency and expressiveness, so choosing between them is largely a question of deciding which of these aspects is most important to you.

## Week Six: Data parallelism using the GPU

CSP was the last of the general-purpose programming models, and for the last two chapters, we looked specifically at data parallelisation.

The first one is using the Graphics Processing Unit (GPU). The GPU is a powerful data-parallel processor, and can be much faster than the CPU when used specifically for number-crunching. This is called general purpose computing on the GPU, or GPGPU (!!)

Computer graphics is all about manipulating data very quickly. A scene in a 3D game is made up of loads of tiny triangles that need to have their position calculated, lit, textured, etc, many times a second, and modern GPUs are capable of manipulating billions of these per second. Although the amount of data that needs to be processed is huge, the relative operations on that data are relatively simple vector or matrix operations, so they are amenable to data parallelisation, where multiple computing units perform the same operations on different items of data in parallel.

Data parallelisation can be implemented in many different ways. The book looks at two: pipelining and multiple ALUs.

- Pipelining. At the level of gates on a chip, something as simple as multiplying 2 numbers takes several steps. It may take say, 5 clock cycles. However, if we have multiple operations, we can just pack them in behind each other and keep it moving. So multiplying a thousand pairs of numbers takes a bit over a thousand clock cycles rather than five thousand clock cycles.
- Multiple ALUs. An ALU is an arithmetic logic unit. If you have a lot of these and a wide memory bus that allows multiple operands to be fetched simultaneously, operations on large amounts of data can be parallelised.

### Each GPU is architected slightly differently

GPUs use a combination of these approaches amd many others to achieve performance, and each GPU is architected slightly differently.

Open Computing Language (OpenCL) abstracts away the details of the GPU implementation by defining a C-like language which allows us to express a parallel algorithm abstractly. Each different GPU manufacturer then provides its own compilers and drivers that allow the program to be compiled and run on its hardware.

To parallelise our array multiplication task we need to divide it into work-items that will be executed in parallel. These are typically very small, as small as they possibly can be (unlike other parallelisation, where you might want to ensure each task is not *too* small so it doesn't waste effort creating threads and communicating). The OpenCL compiler and runtime then worry about how best to schedule these work-items.

We specify how each work-item should be processed by writing an OpenCL kernel. You then need to embed the kernel in a host program. There are C and C++ bindings defined in the OpenCL standard, but there are unofficial bindings for most major languages, so you can write the host program in almost whatever language you like.

A work-item executing a kernel has access to four different memory regions:

- global memory: available to all work-items executing on a device
- constant memory: a region of global memory that remains constant during execution of a kernel
- local memory: memory local to a work-group; can be used for communication between work-items executing in that work-group
- private memory: memory private to a single work-item

The actual implementation of these is specific to the device, and this can have a significant impact when it comes to optimising. This is one of the drawbacks of data parallelisation on the GPU; as this makes it difficult to write cross-platform code. In addition, it's not easily adaptable to non-numeric problems.

However, it's ideal when you have large amounts of numerical data that need to be processed as GPUs are powerful data-parallel processors.

## Week Seven: The Lambda Architecture

GPGPU is data parallelism in the small, i.e. on one computer. The last chapter looks at data parallelisation in the large, i.e. across multiple machines using the Lambda Architecture; and specifically, the batch layer and the speed layer of MapReduce on Hadoop.

MapReduce can mean the common pattern of breaking an algorithm down into two steps: a map over a data structure, followed by a reduce operation. However, it can also mean something more specific: a system that takes an algorithm encoded as a map followed by a reduce, and efficiently distributes it across a cluster of computers. It automatically partitions both the data and its processing, and continues to operate if one or more of these machines fails.

Hadoop is one framework for MapReduce. Its power comes from the fact that it splits data into sections, each of which is then processed by separate machines.

A MapReduce task is constructed from two type of component: mappers and reducers. Mappers take some input format and map it to a number of key/value pairs. Reducers then convert these pairs to the ultimate output format (normally also a set of key/value pairs).

The input typically comprises one or more large text files; Hadoop splits them and send each split to a single mapper. The mapper outputs a number of key/value pairs which Hadoop then sends to the reducers.

The key/value pairs from a single mapper are sent to multiple reducers. Which reducer receives a particular key/value pair is determined by the key. Hadoop guarantees that all pairs with the same key will be processed by the same reducer, no matter which mapper generated them. This is the shuffle phase.

Hadoop calls the reducer once for each key, with a list of all the values associated with it. The reducer combines these values and generates the final output.

Breaking a problem into a map over a data structure followed by a reduce operation makes it easy to parallelise.

Apart from speed, Hadoop has been build from the ground up to handle failure of nodes. It uses the Hadoop distributed file system (HDFS) by default, which is a fault-tolerant files system, that replicates data across multiple nodes; this means it avoids loss of data if one or more disks fail.

Because we are talking about gigabytes or more of data, we are at the point at which it is unreasonable to expect we'll be able to fit intermediate data or results in memory. Hadoop stores key/value pairs within HDFS during processing, allowing us to create jobs that process much larger datasets than will fit in memory.

Taken together, these aspects are transformative, and what allows Hadoop to really handle big data. Throughout the book, we have kept returning to an example of counting words on pages in Wikipedia; MapReduce is the only technology that has allowed us to actually process the entire dump of wikipedia.

### Raw data is eternally true

We can divide information into two categories: raw data and derived information. Raw data is eternally true. So, for example, a home address with a timestamp is data; where you live now is derived information that might change.

If you had an infinitely fast computer then you would only ever store raw data because you could process it however you liked in an instant, and you wouldn't need locking or transactions, because once it's been stored it will never change. This is a fantasy but we can get quite close by leveraging the power of MapReduce.

If we know ahead of time which queries we want to run against our raw data, we can precompute a batch view which either directly contains the derived information that will be returned by those queries, or contains data that can easily be combined to create it. Computing these batch views is the job of the Lambda Architecture's batch layer.

For example, if we wanted a list of my Git commits per day over a year. We don't need to store all of them. Maybe we can precompute two totals: total per day and total per month. We can then sum as required, and if not quite start/end of month we can offset by day.

Because it only ever operates on raw data, data can be distributed across machines. This means the batch view can be recomputed in a reasonable amount of time even with terabytes of data. Raw data also means the system is hardened against technical failure and human error; its much easier to back up raw data but also if there's a bug, we can always just fix the bug and recompute the batch view.

Note: the Lambda Architecture is not tied to MapReduce; the batch layer could be implemented with any batch processing system. He recommends Apache Spark as particularly interesting.

There is one problem: latency. The batch layer could take an hour to run, so your data is always an hour out of date. Hence, the speed layer.

### The speed layer

As new data arrives, we both append it to the raw data that the batch layer works on and also send it to the speed layer. The speed layer generates real-time views, which are combined with the batch views to create fully up-to-date answers to queries. Real time views only contain information derived from the data that arrived since the batch views were last generated, and are discarded when their data is processed by the batch layer.

One way to build a speed layer is as a traditional synchronous database. In fact, you could think of a traditional database application as a case of the Lambda Architecture in which the batch layer never runs. In this approach, clients communicate directly with the database and block while it's processing each update.

Another approach is asynch: clients add updates to a queue (e.g. Kafka) as they arrive and without blocking, and a stream processer then handles these updates in turn and performs the database update. Using a queue decouples clients from database updates, making it more complex to coordinate updates. This might be acceptable for many applications, and where it is, there are a lot of benefits. No blocking means higher throughput. Asynch processing means that spikes in demand just make it fall behind rather than time out or drop updates. Also, the stream processor can exploit parallelism.

### Ping pong

Side note: the speed layer needs to have capacity for twice the amount of time data as the batch is behind, e.g. if the batch later takes one hour to run, the speed layer will need up to two hours, because if the batch layer has just finished, the data is one hour out of date. So the speed layer needs to serve data for the hour it was running, plus any data that comes in while the next one is running.

One common way to handle this is to have two speed layers. Whenever a batch run completes and new data becomes available in the batch views, we switch to the other speed layer, and the one we switched from clears its database and starts building a new set of views – so we never have to worry about which data to delete. This is called ping-pong speed layers.

### The Lambda Architecture ties it all together

The Lambda Architecture brings together many of the concepts from the book, e.g.:

- Raw data being eternally true is reminiscent of Clojure's separation of identity and state
- Hadoop's approach of parallelising a problem by splitting it into a map over a data structure followed by a reduce is reminiscent of parallel functional programming
- Like Actors, the Lambda Architecture distributes processing over a cluster to improve performance and provide fault tolerance

The main weakness of the Lambda Architecture is that if your data is not measured in tens of gigabytes or more, the overhead is unlikely to be worth the benefit.

However, it is a fitting end to the book as it's a powerful demonstration of how parallelism and concurrency allow us to tackle problems that would otherwise be intractable.

### Not everything was covered

The author lists some other techniques that aren't covered in the book, e.g.:

- Fork/join and work-stealing, e.g. Cilk
- dataflow in much detail, mainly because there isn't a good general purpose dataflow language
- Reactive programming, e.g. Rx
- Functional reactive programming, e.g. Elm
- Grid computing, e.g SETI@Home
- Tuple spaces, e.g. Linda

## The author's summary of the book: immutability is key

The author's summary is that the central concept is immutability, because it helps with everything, e.g. raw data, fewer locks etc. And it seems clear that even if you are not writing in a functional language, the frameworks you use and code you write will be increasingly influenced by functional principles, which will allow us to exploit concurrency and parallelism, as well as making code simpler, easier to understand and more reliable.

One reason for the interest in all this is multiple cores. Instead of individual cores becoming faster, we're seeing CPUs with more and more cores, and soon shared memory might be a bottleneck, so we'll have to worry about distributed memory, which he thinks makes it inevitable that techniques based on message-passing will become more important over time.

These thoughts were backed up by [Sophie Wilson's QCon keynote](https://qconlondon.com/london2022/keynote/future-microprocessors). For example, she pointed out the inverse of Moore's law is that you now need [18 times as many scientists working on holding performance constant](https://acquisitiontalk.com/2020/08/more-on-the-slowdown-in-science-and-technology/) than the 1970s. General purpose performance hasn't increased, though it has got more energy efficient – but it costs more. It's now about packaging, rather than getting bigger.

## My summary of the book: extremely interesting

I started reading this on 11th June and finished on 20th October 2021, so not quite seven weeks; in fact it took 18 weeks and 5 days to read, plus a lot more time parsing my notes enough to write this blog post (and then a lot more editing it – the first draft was 15,000 words!)

The book was extremely interesting and challenging. To begin with, I did all the code exercises, and read all the supporting documentation, and really enjoyed the brain exercise: as I no longer write code or have to understand programming documentation in my day to day work, it was fun exercising my brain. For example, I really enjoyed reading [some Clojure documentation](https://clojure.org/reference/special_forms#binding-forms) several times until the lightbulb suddenly came on, and learning new words, like "arity". It made me feel smarter, and reinforced some things I already knew.

However, as I got deeper into the book and time marched on, I ultimately stopped doing all the exercises, as it wasn't clear that I'd ever be able to finish the book at that rate. However, this is definitely a book you could dip into if you wanted more background on any of the areas: it's incredibly detailed and well thought out.

The book was published in 2014, so it's a snapshot in time, but it's still extremely useful to to have this fascinating deeper dive into some areas I knew about but certainly didn't understand the details.

I highly recommend it!
