1. What are the different states of a process?
2. (a) What is virtual memory?
   (b) What is thrashing?
3. What is Belady's Anomaly?
4. What is starvation? Explain aging in Operating System.
5. What are the differences between Real Time System and Timesharing System?
6. Explain SMP.
7. What is the difference between logical address space and physical address space?
8. Discuss about spooling.
9. Differentiate between paging and segmentation.
10. Differentiate the following:
    a) Logical and physical address space.
    b) Process and thread.
11. What is the purpose of interrupts? What are the differences between a trap and an interrupt?
12. Describe Banker's algorithm. Describe the following data structure: Need, Allocation, Max, Available.
13. What is a thread? Write three points to differentiate it from process.
14. Explain the difference between internal and external fragmentation.
15. Define Thread and compare fork() and clone().
16. What is Belady’s Anomaly? Explain with an example.
17. Compare CSCAN and CLOOK disk arm scheduling algorithms with examples.
18. Explain with examples the difference between preemptive and non-preemptive priority scheduling.
19. Distinguish between starvation and deadlock.
20. a) What is an Operating System? What are the functions of Operating System?
    b) Explain "multitasking is logical extension of multiprogramming".
21. Describe shared resource system and message passing system.
22. What is race condition? Explain Peterson solution for avoiding race condition.
23. Explain PCB.
24. Define thread and its life cycle.
25. What do you mean by Critical Section Problem? Explain with example.
26. Explain Demand Paging in memory management scheme. What is Multilevel Feedback Queue?
27. What is page fault? When does it occur?
28. Explain State Transition Diagram of a Process.
29. What are the necessary and sufficient conditions for deadlock to occur? What is thrashing?
30. What do you mean by Race Condition with respect to Producer – Consumer Problem? Explain how Race Condition can be avoided.
31. A computer provides each process with 65536 bytes of address space divided into 4096 bytes. A particular program has text size of 32768 bytes, data size of 16386 bytes and stack size of 15870 bytes. Will this program fit in the address space? If the page size were of 512 bytes, would it fit? Give reasons for all your answers.
32. Different memory partitions of 150K, 820K, 360K and 350K (in the given order) are present. Explain how best fit algorithm can be used to place a process of 315K. What are the advantages and disadvantages of using best fit over worst fit and first fit algorithms?
33. a) When does a page-fault occur?
    b) Describe the action taken by the operating system when a page fault occurs.
34. Explain PCB with a neat diagram.
35. Explain three types of CPU schedulers and compare the execution frequency of these three types of schedulers.
36. Explain Monolithic, Layered and Microkernel architectures of an Operating System.
37. What are Processors, Memory, Devices, and I/O Bus in a computer system and draw a diagram showing interconnection and data flow direction among these components.
38. Explain: Batch, Time-sharing, Distributed and Real-time Operating System.
39. Explain: Multi-tasking, Multi-programming, Multi-processing OS.






1. What are the different states of a process?
   A process in an operating system goes through various states during its lifetime. The primary states include New, Ready, Running, Waiting, and Terminated. When a process is created, it enters the New state. Once it is ready for execution, it moves to the Ready state. The scheduler selects a process from the Ready queue to execute, changing its state to Running. If the process needs to wait for resources like I/O, it moves to the Waiting state. Once the process completes or is terminated by the system, it enters the Terminated state. These transitions are managed by the OS scheduler and are crucial for process management.

2. (a) What is virtual memory?
   Virtual memory is a memory management technique that gives an application the impression it has contiguous memory, while in reality, it may be fragmented and even stored on disk. It allows systems to run larger applications than the available physical memory by using disk space as an extension of RAM. (b) What is thrashing?
   Thrashing occurs when a system spends more time swapping pages in and out of memory than executing actual processes. It usually happens when there is insufficient RAM, and processes continuously cause page faults.

3. What is Belady's Anomaly?
   Belady's Anomaly is a phenomenon where increasing the number of page frames results in an increase in the number of page faults in some page replacement algorithms like FIFO. This behavior is counterintuitive because one would expect more memory to reduce faults. It highlights inefficiencies in certain algorithms and is used to justify the use of more advanced page replacement strategies like LRU or Optimal.

4. What is starvation? Explain aging in Operating System.
   Starvation in operating systems occurs when a low-priority process waits indefinitely to get CPU time or resources because higher-priority processes keep getting scheduled. Aging is a technique used to prevent starvation by gradually increasing the priority of waiting processes over time, ensuring that they eventually get scheduled for execution.

5. What are the differences between Real Time System and Timesharing System?
   Real-time systems are designed to respond to inputs or events within a strict time deadline, and missing the deadline can lead to failure. They are used in critical applications like medical systems and industrial controls. Time-sharing systems, on the other hand, allow multiple users to share system resources simultaneously, giving each user a time slice of CPU. These systems focus on fairness and responsiveness rather than strict timing.

6. Explain SMP.
   Symmetric Multiprocessing (SMP) is a system architecture where multiple processors share a common memory and operate under a single operating system. Each processor performs tasks independently but can communicate and share data with other processors. SMP improves performance and reliability by allowing parallel processing and load balancing across CPUs.

7. What is the difference between logical address space and physical address space?
   Logical address space refers to the set of addresses generated by a program's perspective during execution, while physical address space refers to the actual locations in the main memory. The operating system, with the help of the memory management unit, translates logical addresses to physical addresses during program execution to ensure proper access and isolation.

8. Discuss about spooling.
   Spooling is a process where data is temporarily gathered in a buffer so that a device like a printer or disk can access it at its own pace. It helps in managing input/output operations by allowing devices to operate asynchronously with the CPU. Spooling is commonly used in printing systems to queue print jobs efficiently.

9. Differentiate between paging and segmentation.
   Paging is a memory management technique where memory is divided into fixed-size pages and frames. It eliminates external fragmentation. Segmentation, on the other hand, divides memory into variable-sized segments based on logical divisions such as functions or arrays. While paging focuses on physical memory management, segmentation aligns with the logical structure of programs.

10. Differentiate the following:
    a) Logical and physical address space: Logical address space is the address generated by the CPU during program execution, and physical address space is the actual location in the physical memory where data is stored.
    b) Process and thread: A process is an independent program in execution with its own memory space, while a thread is a lightweight process that shares memory with other threads of the same process.

11. What is the purpose of interrupts? What are the differences between a trap and an interrupt?
    Interrupts signal the CPU to stop its current execution and address an urgent task, improving system responsiveness. A trap is a software-generated interrupt typically used for system calls or errors, whereas an interrupt is usually hardware-generated to signal events like I/O completion.

12. Describe Banker's algorithm. Describe the following data structure: Need, Allocation, Max, Available.
    Banker's algorithm is a deadlock avoidance method that ensures a system only grants resources if it remains in a safe state. It uses data structures: Allocation (resources currently allocated to processes), Max (maximum resources a process may need), Need (Max - Allocation), and Available (resources currently available). It simulates resource allocation and checks system safety before committing.

13. What is a thread? Write three points to differentiate it from process.
    A thread is the smallest unit of CPU execution within a process. Differences: Threads share memory, processes do not; thread creation is faster than process creation; communication between threads is easier due to shared memory.

14. Explain the difference between internal and external fragmentation.
    Internal fragmentation occurs when memory is allocated in fixed-sized blocks and some part of the block remains unused. External fragmentation happens when there is enough total free memory, but it is scattered in small non-contiguous blocks, making it difficult to allocate to new processes.

15. Define Thread and compare fork() and clone().
    A thread is a unit of execution within a process that shares memory and resources. fork() creates a new process with a separate memory space, while clone() can create threads or processes depending on flags and allows sharing of memory, file descriptors, and more.

16. What is Belady’s Anomaly? Explain with an example.
    Belady’s Anomaly occurs in FIFO page replacement where increasing the number of page frames results in more page faults. For example, a reference string 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5 causes fewer faults with three frames than four, illustrating the anomaly.

17. Compare CSCAN and CLOOK disk arm scheduling algorithms with examples.
    CSCAN moves the disk arm in one direction, servicing requests, and jumps back to the beginning once it reaches the end. CLOOK is similar but only goes as far as the last request before jumping back. CSCAN ensures uniform wait time, while CLOOK reduces unnecessary traversal.

18. Explain with examples the difference between preemptive and non-preemptive priority scheduling.
    In preemptive scheduling, a higher-priority process can interrupt a running lower-priority one. In non-preemptive scheduling, once a process starts, it runs until completion. For example, if a high-priority process arrives while a low-priority one runs, it takes over in preemptive, but waits in non-preemptive.

19. Distinguish between starvation and deadlock.
    Starvation occurs when a process waits indefinitely due to low priority. Deadlock is a situation where a group of processes are waiting on each other indefinitely. In starvation, some processes still run; in deadlock, none can proceed.

20. a) What is an Operating System? What are the functions of Operating System?
    An operating system is system software that manages hardware and software resources. Its functions include process management, memory management, file system management, device control, and security.
    b) Explain "multitasking is logical extension of multiprogramming".
    Multitasking builds on multiprogramming by allowing processes to execute seemingly simultaneously through CPU scheduling, increasing system interactivity.

21. Describe shared resource system and message passing system.
    Shared resource systems allow processes to access common memory or devices. Message passing systems enable processes to communicate and synchronize by sending and receiving messages, often used in distributed systems.

22. What is race condition? Explain Peterson solution for avoiding race condition.
    Race condition occurs when two or more processes access shared data and try to change it simultaneously. Peterson’s algorithm solves this by using two shared variables to ensure mutual exclusion between two processes.

23. Explain PCB.
    A Process Control Block (PCB) is a data structure used by the OS to store information about a process. It includes process ID, state, program counter, registers, memory limits, and accounting information. The OS uses PCB to manage processes.

24. Define thread and its life cycle.
    A thread is a lightweight process that shares resources with other threads of the same process. The life cycle of a thread includes New, Ready, Running, Waiting, and Terminated states, similar to processes.

25. What do you mean by Critical Section Problem? Explain with example.
    The critical section problem involves ensuring that only one process accesses shared data at a time to avoid inconsistency. For example, two processes updating a shared counter must not enter the critical section simultaneously.

26. Explain Demand Paging in memory management scheme. What is Multilevel Feedback Queue?
    Demand paging loads pages into memory only when needed, reducing memory usage. Multilevel Feedback Queue is a CPU scheduling method where processes move between queues based on their behavior and age to improve responsiveness and fairness.

27. What is page fault? When does it occur?
    A page fault occurs when a process tries to access a page that is not currently in physical memory. It happens when the required page is not in memory, prompting the OS to fetch it from disk.

28. Explain State Transition Diagram of a Process.
    The state transition diagram illustrates how a process changes states: New → Ready → Running → Waiting → Terminated. Transitions occur based on events like scheduler selection, I/O requests, or process termination.

29. What are the necessary and sufficient conditions for deadlock to occur? What is thrashing?
    The four conditions for deadlock are mutual exclusion, hold and wait, no preemption, and circular wait. Thrashing is when excessive paging causes little or no actual processing due to constant page faults.

30. What do you mean by Race Condition with respect to Producer – Consumer Problem? Explain how Race Condition can be avoided.
    In the Producer–Consumer problem, race condition occurs when both access the shared buffer simultaneously. It can be avoided using synchronization tools like mutexes or semaphores to ensure mutual exclusion.

31. A computer provides each process with 65536 bytes of address space divided into 4096 bytes. A particular program has text size of 32768 bytes, data size of 16386 bytes and stack size of 15870 bytes. Will this program fit in the address space? If the page size were of 512 bytes, would it fit? Give reasons for all your answers.
    Total space needed is 32768 + 16386 + 15870 = 65024 bytes, which is less than 65536 bytes, so it fits. With 512-byte pages, total pages needed = 64 (32768) + 33 (16386) + 31 (15870) = 128 pages. Since 65536 / 512 = 128 pages available, it fits perfectly.

32. Different memory partitions of 150K, 820K, 360K and 350K (in the given order) are present. Explain how best fit algorithm can be used to place a process of 315K. What are the advantages and disadvantages of using best fit over worst fit and first fit algorithms?
    Best fit finds the smallest partition that fits the process. Here, 360K is the best fit for 315K. Advantages: less internal fragmentation. Disadvantages: can lead to small unusable holes, and takes more time than first fit.

33. a) When does a page-fault occur?
    A page fault occurs when the accessed page is not in memory.
    b) Describe the action taken by the operating system when a page fault occurs.
    The OS pauses the process, loads the page from disk to memory, updates page tables, and resumes the process.

34. Explain PCB with a neat diagram.
    A PCB includes process ID, state, program counter, CPU registers, memory information, and accounting info. It helps the OS track process execution. Diagram typically includes these fields linked together.

35. Explain three types of CPU schedulers and compare the execution frequency of these three types of schedulers.
    Long-term scheduler controls job admission, medium-term swaps jobs in/out of memory, and short-term selects ready processes for CPU. Short-term runs frequently, long-term runs less often, and medium-term runs occasionally.

36. Explain Monolithic, Layered and Microkernel architectures of an Operating System.
    Monolithic architecture includes all OS services in one layer. Layered architecture separates services into layers with defined functions. Microkernel architecture keeps only essential services in the kernel, others run in user space for better modularity.

37. What are Processors, Memory, Devices, and I/O Bus in a computer system and draw a diagram showing interconnection and data flow direction among these components.
    Processors perform computations. Memory stores data. Devices interact with users. I/O bus connects these components and allows data flow. Diagram shows CPU ↔ Memory ↔ Devices via I/O bus.

38. Explain: Batch, Time-sharing, Distributed and Real-time Operating System.
    Batch OS executes jobs in batches with no user interaction. Time-sharing OS allows multiple users to share the system. Distributed OS manages multiple machines as one. Real-time OS meets strict timing constraints.

39. Explain: Multi-tasking, Multi-programming, Multi-processing OS.
    Multitasking runs multiple tasks simultaneously for a user. Multiprogramming loads many programs into memory to utilize CPU efficiently. Multiprocessing uses multiple CPUs for parallel processing.

