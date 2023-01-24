# Operating Systems

## Basic Concepts
```
linux process example
```
ps -ef
UID User ID
PID (process Id) – this is the 5-digit number assigned by OS for a process. No PID can be the same.
PPID (parent process Id) – PID of the parent process
CPU utilization of process
STIME – Process start time
TTY – the Terminal type associated with the process
CMD – the command that started that process
kill: Used to a process whose PID is known
```
types of processes
```
1. Parent process: process created by the user on the terminal. All processes have a parent process, If it was created directly by user then the parent process will be the kernel process
2. Child process: process created by another process (by its parent process)
3. Orphan process: Sometimes when the parent gets executed before its own child process then the child process becomes an orphan process
4. Zombie process: processes which are already dead but shows up in process status is called Zombie process
5. Daemon process: system-related processes that run in the background
```
high level overview
```
- Abstractions (process, thread, file, socket, memory)
- Mechanisms (create, schedule, open, write, allocate)
- Policies (LRU, EDF)
- Separation of mechanism and policy by implementing flexible mechanisms to support policies
- Monolithic OS, where the entire OS is working in kernel space and is alone in supervisor mode
- Modular OS, in which some part of the system core will be located in independent files called modules that can be added to the system at runtime
- Micro OS, where the kernel is broken down into separate processes, known as servers. Some of the servers run in kernel space and some run in user-space
```
processes
```
- Stack: The process Stack contains the temporary data such as method/function parameters, return address and local variables
- Heap: This is dynamically allocated memory to a process during its run time
- Text: This includes the current activity represented by the value of Program Counter and the contents of the processor's registers
- Data: This section contains the global and static variables
- Start: This is the initial state when a process is first started/created
- Ready: The process is waiting to be assigned to a processor
- Running: Once the process has been assigned to a processor by the OS scheduler, the process state is set to running and the processor executes its instructions
- Waiting: Process moves into the waiting state if it needs to wait for a resource, such as waiting for user input, or waiting for a file to become available
- Terminated: Once the process finishes its execution, or it is terminated by the operating system, it is moved to the terminated state where it waits to be removed from main memory
- Process State: The current state of the process
- Process Privileges: This is required to allow/disallow access to system resources
- Process ID: Unique identification for each of the process in the operating system
- Pointer: A pointer to parent process
- Program Counter: Program Counter is a pointer to the address of the next instruction to be executed for this process.
- CPU Registers: Various CPU registers where process need to be stored for execution for running state
- CPU Scheduling Information: Process priority and other scheduling information which is required to schedule the process.
- Memory Management Information: This includes the information of page table, memory limits, Segment table depending on memory used by the operating system
- Accounting Information: amount of CPU used for process execution, time limits, execution ID
- IO Status Information: list of I/O devices allocated to the process
```
threads
```
- Threads minimize the context switching time
- Use of threads provides concurrency within a proces
- Threads allow utilization of multiprocessor architectures
- Threads are implemented as user level threads or kernel level threads
```
scheduling
```
- Job queue keeps all the processes in the system
- Ready queue keeps a set of all processes residing in main memory, ready and waiting to execute
- Device queue is all processes which are blocked due to unavailability of an I/O device constitute this queue

```
mm
```
Functionality of an operating system which handles or manages primary memory and moves processes back and forth between main memory and disk during execution
- addresses can range from 0 to 0x7fffffff; that is, 2^31 possible numbers which is 2gb of information
- Symbolic addresses: The addresses used in a source code. The variable names, constants, and instruction labels are the basic elements of the symbolic address space
- Relative addresses: At the time of compilation, a compiler converts symbolic addresses into relative addresses
- Physical addresses: The loader generates these addresses at the time when a program is loaded into main memory
- Virtual and physical addresses are the same in compile-time and load-time address-binding schemes. Virtual and physical addresses differ in execution-time address-binding scheme
- set of all logical addresses generated by a program is referred to as a logical address space
- set of all physical addresses corresponding to these logical addresses is referred to as a physical address space
```
ipc
```
A mechanism which allows processes to communicate each other and synchronize their actions. Processes can communicate with each other using Shared Memory, Message Parsing Method.
```
io mngmnt
```
One of the important jobs of an Operating System is to manage various I/O devices including mouse, keyboards, touch pad, disk drives, display adapters, USB devices, Bit-mapped screen, LED, Analog-to-digital converter, On/off switch, network connections, audio I/O, printers
- Block devices - A block device is one with which the driver communicates by sending entire blocks of data. For example, hard disks, USB cameras, Disk-On-Key etc
- Character Devices - A character device is one with which the driver communicates by sending and receiving single characters (bytes, octets). For example, serial ports, parallel ports, sounds cards
```
si io
```
This uses CPU instructions that are specifically made for controlling I/O devices. These instructions typically allow data to be sent to an I/O device or read from an I/O device.
```
mem io
```
- When using memory-mapped I/O, the same address space is shared by memory and I/O devices. The device is connected directly to certain main memory locations so that I/O device can transfer block of data to/from memory without going through CPU
- While using memory mapped IO, OS allocates buffer in memory and informs I/O device to use that buffer to send data to the CPU. I/O device operates asynchronously with CPU, interrupts CPU when finished
- The advantage to this method is that every instruction which can access memory can be used to manipulate an I/O device. Memory mapped IO is used for most high-speed I/O devices like disks, communication interfaces
```
dma
```
- CPU grants I/O module authority to read from or write to memory without involvement. DMA module itself controls exchange of data between main memory and the I/O device. CPU is only involved at the beginning and end of the transfer and interrupted only after entire block has been transferred.

- DMA controller (DMAC) that manages the data transfers and arbitrates access to the system bus. The controllers are programmed with source and destination pointers (where to read/write the data), counters to track the number of transferred bytes, and settings, which includes I/O and memory types, interrupts and states for the CPU cycles.
```
virtualization
```
- Data Virtualization: data spread all over can be consolidated into a single source
- Desktop Virtualization: perform mass configurations, updates, and security checks on all virtual desktops
- Server Virtualization: process a high volume of specific tasks
- OS Virtualization: virtualization happens at kernel
- Network Functions Virtualization: network key functions like directory services, file sharing, and IP configuration so they can be distributed
```
dfs
```
A client/server-based application that allows clients to access and process data stored on the server as if it were on their own computer
```
dsm
```
A resource management component of a distributed operating system that implements the shared memory model in distributed systems, which have no physically shared memory
```

## Types of operating systems
Single-tasking and multi-tasking  
Single- and multi-user  
Distributed  
Templated  
Embedded  
Real-time  
Library  

## Components
Mainframe vs Microcomputer  
Kernel  
Program execution  
Interrupts  
Modes  
Memory management  
Virtual memory  
Multitasking  
Disk access and file systems  
Device drivers  
Networking  
Security  
User interface  
Graphical user interfaces  

## Operating System Concretions
Unix and Unix-like operating systems  
BSD and its descendants  
macOS  
Linux  
Microsoft Windows  
