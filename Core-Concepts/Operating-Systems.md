# Operating System (OS)

## 1) Basic Background

Operating System is an interface between user and the computer hardware, managing the CPU, memory, storage and devices while providing services like process execution and file management.

The CPU has two components:

- **Control Unit** - It fetches and decodes instructions, and sends control signals to coordinate the ALU, registers, and memory. It sequences **micro-operations** using the system clock; the clock’s **frequency** sets execution speed (e.g., **3 GHz = 3×10⁹ cycles/second**). Each clock cycle advances instruction execution in a precise, synchronized manner.
- **Arithmetic Logic Unit/Functional Unit** - It performs arithmetic operations (add, subtract, multiply, divide) and logical operations (AND, OR, NOT, compare) on data. It executes the micro-operations specified by the control unit, producing results and status flags (zero, carry, overflow) within one or more clock cycles.

Memory in an operating system is of two types:

- Primary Memory - volatile, faster to access, smaller, temporary. Ex- RAM, ROM, Cache, Register
- Secondary Memory - non volatile, slower, less expensive. Ex- SSD, HDD, Pen-Drive.

## 2) Types of Software:

1. System Software - Set of programs essential for running the system/device and are present across all users on the system. example- CMD, Windows, DOS
2. Application Software - Programs created for the end user made to perform particular tasks. example- Zoom, MySQL, Gmail
3. Firmware - Software that is stored on the computer’s motherboard or chipset, it runs before the operating system and ensures the device is working correctly. it is the BIOS.
4. Driver Software - Driver software communicates with hardware and control devices and peripherals attached to a computer. It does this by gathering input from the OS (operating system) and giving instructions to the hardware to perform an action or other designated task.

### **Difference between CLI and GUI**

|Basis of Comparison|Command Line Interface (CLI)|Graphical User Interface (GUI)|
|---|---|---|
|Interface Type|Text-based interface|Graphical interface|
|Control|Provides greater control over the system|Limited control over the system|
|Resource Consumption|Lightweight and efficient|Resource-intensive|
|Automation|Automation-friendly|Not as automation-friendly|
|Speed|Faster for experienced users who know the specific commands|Slower for experienced users|

CPU accesses only the primary memory, this is because the secondary memory is very slow and instructions have to be executed sequentially. Files for execution by the CPU are moved from secondary memory to the primary memory using the Operating System.

**Kernel** - is the core part of OS that directly controls the CPU, memory, and hardware, and lets programs safely use these resources. Linux is a kernel.

### Kernel Architecture

- **Monolithic Kernels:** This structure places all functionality—the CPU scheduler, memory manager, file systems, and device drivers—into a single, static binary file that runs in a single address space.
    - _Advantage:_ Speed. Because everything is in one address space, there is no need for context switches or complex message passing when one subsystem needs to communicate with another.
    - _Example:_ Linux and traditional UNIX.
- **Microkernels Kernels:** This approach moves as many non-essential components as possible from the kernel into "user space," leaving only a minimal kernel.
    - _Mechanism:_ Communication between user-level services (like the file system) and the kernel happens via **message passing**.
    - _Advantage:_ It is easier to extend the OS or port it to new hardware, and it is more secure; if a service crashes, it does not take down the entire system.
    - _Example:_ Mach, QNX

## 3) Types of Operating Systems:

Modern OSes can be **multiprogramming + multitasking + multiuser + multiprocessing** at the same time.

- **Uni Programming Operating System**: only one program can be loaded into the memory
- **Batch Operating System:** Executes similar jobs in groups (batches) without user interaction.
- **Time-Sharing/Multitasking Operating System:** Allows multiple users to share resources simultaneously by switching between tasks rapidly. **eg -Linux, Windows, MacOS**
- **Real-Time Operating System (RTOS):** Used when strict time constraints are required (e.g., in air traffic control, robotics).
- **Multiprogramming Operating System:** Increases CPU usage (and efficiency) by keeping multiple jobs in memory, ensuring the CPU always has a task. eg - IBM OS/360
- **Multiprocessing Operating System:** Uses two or more CPUs (processors) within a single system to increase computing power.
- **Distributed Operating System:** Manages multiple, physically separate nodes to appear as one cohesive system
- **Network Operating System:** Runs on a server and provides the ability to manage data, users, and security across a network.

**Throughput** is number of items being executed by the CPU per minute. At one time, CPU can only work on a single program, even for multiprocessors CPUs, only one program will run at gone time in a CPU.

### **Types of Multiprogramming OS:**

1. **Non Pre-emptive**: Does not have the control of the CPU once a process is allocated. drawbacks include Starvation and Lack of Interaction
2. P**re-emptive**: the OS can forcibly take the CPU away from running a process. Preemption means the CPU will allocate tasks based on time or priority ex: modern systems like Windows 7,8,+ and macOS.

## 4) Components of a Single Process

A **program** is a passive entity (a file on a disk), while a **process** is an active entity-it is a program in execution (in the RAM).

#### **Process Memory Layout:** A process is divided into four main sections in memory:

1. **Text Section:** The executable code.
2. **Data Section:** Global and static variables.
3. **Heap:** Memory dynamically allocated during runtime, grows upwards.
4. **Stack:** Temporary data like function parameters and return addresses.

The stack and heap grow towards each other and the OS ensures they never overlap,

**The Process Control Block (PCB):** Every process is represented by a **PCB**, which acts like its "ID card". It stores the _process state, program counter (address of the next instruction), CPU registers (like General Purpose Registers), and memory-management information._

### **Process States, Context Switching, and the Dispatcher**

**Processes** transition through various **states** during their life cycle:

1. **New:** The process is being created.
2. **Ready:** The process is in memory, waiting to be assigned to the CPU.
3. **Running:** Instructions are being executed.
4. **Waiting (Blocked):** The process is waiting for an event, like I/O completion.
5. **Terminated:** The process has finished execution.

### The seven-state model (driven by the need to manage the **degree of multiprogramming** and performance) introduces two new states located on the **hard disk**:

1. **Suspend Blocked (Blocked-Suspended)**

When a process is already in the **Blocked** state (waiting for I/O) and the OS needs to free up RAM for more active tasks, the **Medium-Term Scheduler** "swaps out" the process to the disk.

- **Logical Status:** It is still waiting for its I/O event to complete, but it is physically doing so on the disk rather than in RAM.
- **The "Why":** It is inefficient to keep a process in expensive RAM if it isn't even eligible to run yet.

1. **Suspend Ready (Ready-Suspended)**

This state contains processes that are **logically ready to run** (their I/O is complete) but are **physically located on the disk**.

- **How it's reached:** A process can enter this state if a **Suspend Blocked** process finishes its I/O while still on the disk, or if the OS decides to suspend a process directly from the **Ready** state to manage memory.
- **Re-entry:** A process in this state must be **swapped or loaded** back into the RAM (the Ready state) before the CPU can execute it again.

### **Critical Transitions in the Seven-State Model**

Understanding the flow between these states is vital for your numerical and conceptual questions:

1. **Blocked** → **Suspend Blocked:** Triggered by the **Medium-Term Scheduler** when RAM is full.
2. **Suspend Blocked** → **Suspend Ready:** Occurs when the I/O event the process was waiting for finally completes while the process is still on the disk.
3. **Suspend Ready** → **Ready:** Known as **Swapping or Loading**. The OS brings the process back into RAM so it can be scheduled.
4. **Ready** → **Suspend Ready:** The OS may choose to suspend a ready process if high-priority tasks need the space.
5. **Running** → **Suspend Ready:** While possible (e.g., if a process's time quantum expires and the OS immediately swaps it out), this is generally **undesirable**.

#### **Context Switching:**

When the OS switches the CPU from one process to another, it must perform a **context switch**. This involves saving the current state of the running process into its PCB and loading the saved state of the next process. This is **pure overhead** because the system does no "useful" work while switching.

#### **The Dispatcher:**

The **dispatcher** is the module that actually gives control of the CPU to the process selected by the scheduler. The time it takes to stop one process and start another is called **dispatch latency**

## **5) CPU Scheduling**

The **Ready Queue** is a list of all processes that are in memory and prepared to run on the CPU. It is typically implemented as a linked list where the header points to the first PCB.

**Conditions for Scheduling:**

1. Running → Waiting (e.g., I/O request).
2. Running → Ready (e.g., an interrupt).
3. Waiting → Ready (e.g., I/O completion).
4. Termination.

**Preemptive vs. Non-Preemptive Scheduling:**

- **Non-Preemptive (Cooperative):** Once the CPU is allocated to a process, it keeps it until it either terminates or moves to a waiting state. It releases the CPU voluntarily.
- **Preemptive:** The OS can forcefully take the CPU away from a process (e.g., when a higher-priority process arrives or a time slice expires). This is essential for interactive systems and real-time response.

### **Comprehensive Scheduling Algorithms**

1. **First-Come, First-Served (FCFS):** Simple FIFO queue. It is non-preemptive but can suffer from the **convoy effect**, where short processes wait for one long process to finish.
2. **Shortest-Job-First (SJF):** Chooses the process with the smallest next CPU burst. It is **provably optimal** for minimum average waiting time, but it's hard to implement because we cannot know future burst lengths.
3. **Shortest-Remaining-Time-First (SRTF):** The preemptive version of SJF. If a new process arrives with a burst shorter than the current process's remaining time, the current one is preempted.
4. **Round Robin (RR):** This is a preemptive algorithm designed for time-sharing systems.

- **Working:** Each process is assigned a **time quantum** (typically 10–100ms). The ready queue is treated as a circular FIFO queue.
- **Preemption:** If a process does not finish within its quantum, the dispatcher saves its context to the PCB and moves it to the back of the ready queue.
- **Quantum Impact:** If the quantum is too large, RR behaves like First-Come, First-Served (FCFS). If too small, the system suffers from high context-switching overhead (dispatch latency).

1. **Longest Job First (LJF/LRTF):** Opposite of SJF; it favors longer processes. The preemptive version (LRTF) is tricky because it often switches between processes with equal remaining times to keep them balanced.
2. **Highest Response Ratio Next (HRRN):** This is a **non-preemptive** strategy designed to solve the problem of **starvation** in algorithms like Shortest Job First (SJF).

- **Formula:** _Response_ _Ratio_= (_Waiting_ _Time_ +_Service_ _Time)/Service_ _Time_ .
- **Logic:** As a long process waits in the queue, its "Waiting Time" increases, which eventually gives it a high enough response ratio to be scheduled, even if shorter jobs are present.

1. **Priority Scheduling:** A priority number is assigned to each process. High-priority processes run first. A major risk is **starvation** for low-priority tasks, which is solved by **aging** (gradually increasing priority as a process waits).
2. **Multilevel Queue Scheduling(MLQ):** The ready queue is partitioned into several separate queues (e.g., foreground vs. background) with their own algorithms.
3. **Multilevel Feedback Queue (MLFQ) Scheduling:** The most general algorithm. It allows processes to **move between queues** based on their behavior (e.g., I/O-bound processes move to higher-priority queues, while CPU-bound ones sink lower)

## 6) Gantt Chart

**1. The Mathematical Foundation: Process Times**

Before looking at algorithms, you must be fluent in these six metrics used to evaluate scheduler performance:

- **Arrival Time (AT):** The moment a process enters the **Ready Queue**.
- **Burst Time (BT):** The total CPU time required by the process for one cycle.
- **Completion Time (CT):** The time at which the process finishes its execution.
    - **Formula:** CT=A_T+BT_ (only for the first process). For P2, if CT1<AT2, then CT2 = AT2 + BT2, otherwise CT2 = CT1 + BT
- **Turnaround Time (TAT):** The total time spent in the system.
    - **Formula:** _TAT_=_CT_−_AT_.
- **Waiting Time (WT):** The time a process spends waiting in the ready queue.
    - **Formula:** _WT_=_TAT_−_BT_.
- **Response Time (RT):** The time from submission until the **first** response is produced (crucial for interactive systems).

## 7) Threads and Concurrent Programming

**Threads VS Process:**

- **Process:** It is a **"program in execution", w**hile a program is a passive entity (like a file on a disk), a process is an **active entity** with the next instruction and a set of associated resources. A process is the primary unit of work in a system, it exists as an independent unit of execution.

Since processes have separate memory, they must use complex **Inter-Process Communication (IPC)** mechanisms like shared memory or message passing to exchange data

- **Thread:** Defined as the **basic unit of CPU utilization**. Modern operating systems allow a single process to contain multiple threads of control, enabling it to perform more than one task at a time. Threads are often called **"lightweight processes".** Threads are **not independent**; they are cooperating parts of a single process. If a process terminates or crashes, **all of its constituent threads die** with it

Because threads share the same address space by default, they can communicate very easily using **Global Variables**, which is much more efficient than IPC

---

A **thread** is the basic unit of CPU utilization, comprising a thread ID, program counter (PC), register set, and a stack. While a traditional process has a single thread of control, modern systems support **multithreading**, allowing a process to perform multiple tasks simultaneously.

- **Advantages:** Multithreading provides **responsiveness** (the app stays active even if one part is blocked), **resource sharing** (threads share the process's code and data by default), **economy** (creating threads is significantly cheaper than creating processes), and **scalability** (utilizing multicore architectures).
- **Categorization:**
    - **User-Level Threads:** Managed without kernel support; they offer faster context switching but can cause the entire process to block if one thread makes an I/O call.
    - **Kernel-Level Threads:** Managed directly by the OS; they support true parallelism on multiple CPUs but have higher overhead.
- **Concurrent vs. Parallel:** **Concurrency** exists when multiple tasks make progress over time (interleaved execution), while **parallelism** exists when multiple tasks run simultaneously on different cores.

## 8) Process Synchronization

When multiple processes or threads access shared data concurrently, a **race condition** can occur, where the final result depends on the specific order of execution

**The Three Mandatory Conditions for a Solution:**

1. **Mutual Exclusion:** Only one process can be in the **critical section** at a time.
2. **Progress:** If no process is in the critical section, only those wanting to enter can decide who goes next; this cannot be delayed indefinitely.
3. **Bounded Waiting:** There must be a limit on how many times other processes can enter their critical sections after a process has made a request.

**Key Solutions:**

- **Peterson’s Solution:** A classic two-process software solution using **`flag`** and **`turn`** variables to ensure all three requirements are met.
- **Semaphores:** OS-level tools. **Binary semaphores** (mutexes) take values 0 or 1, while **counting semaphores** can track finite resources.
    - _Numerical Insight:_ If a counting semaphore _S_ is initialized to 10 and 6 _P_ (wait) operations and 4 _V_ (signal) operations are performed, the final value is 10−6+4=8.
- **Monitors:** High-level synchronization constructs that encapsulate shared data and force mutual exclusion at the language level.

## 9) Deadlocks

A **deadlock** is a state where every process in a set is waiting for an event that only another process in the set can cause.

**The Four Necessary Characteristics (Must hold simultaneously):**

1. **Mutual Exclusion:** Non-sharable resources.
2. **Hold and Wait:** Holding one resource while waiting for another.
3. **No Preemption:** Resources cannot be forcibly taken.
4. **Circular Wait:** A closed chain of processes waiting on each other.

**Handling Strategies:**

- **Prevention:** Constrain resource requests to ensure at least one condition (usually Circular Wait) cannot hold.
- **Avoidance (Banker’s Algorithm):** The OS uses a priori information about maximum possible requirements to ensure the system always stays in a **safe state** (a sequence exists to satisfy all processes).
- **Detection and Recovery:** Periodically check for cycles in a **Resource-Allocation G.**

## 10) Memory Management

The **Memory Management Unit (MMU)** maps **logical addresses** (generated by the CPU) to **physical addresses** (actual RAM locations).

- **Contiguous Allocation:**
    - **Fixed Partitioning:** Memory is divided into set blocks; causes **internal fragmentation** (wasted space within a partition).
    - **Variable Partitioning:** Partitions are created dynamically; causes **external fragmentation** (total free space exists but is not contiguous).
    - **Allocation Strategies:** **First-fit** (first hole big enough), **Best-fit** (smallest hole that fits), and **Worst-fit** (largest hole).
- **Non-Contiguous Allocation:**
    - **Paging:** Logical memory is divided into **pages** and physical memory into **frames**. It eliminates external fragmentation but can have internal fragmentation on the last page.
    - **Segmentation:** Memory is divided into logical units (code, data, stack) reflecting the programmer's view.

## 11) Virtual Memory and Page Replacement

**Virtual memory** allows the execution of processes that are not completely in physical memory, enabling programs to be larger than the actual RAM. This is typically implemented via **demand paging**.

- **Page Fault:** Occurs when the CPU tries to access a page marked "invalid" (not in RAM), triggering the OS to bring it from the backing store.
- **Thrashing:** High paging activity where the system spends more time swapping pages than executing instructions, caused by over-allocating processes.

**Page Replacement Algorithms:**

- **FIFO (First-In, First-Out):** Replaces the oldest page. Suffers from **Belady’s Anomaly** (page faults can increase even if you add more frames).
- **Optimal (OPT):** Replaces the page that will not be used for the longest time in the future. Provably optimal but impossible to implement practically.
- **LRU (Least Recently Used):** Replaces the page not used for the longest time in the past. It is generally considered a high-performance standard.
- **MRU (Most Recently Used):** Replaces the page that was just accessed