# System Calls

A **system call** is a mechanism that allows a program to request a service from the **operating system’s kernel**.  
It serves as a bridge between user-space applications and the OS, enabling controlled access to hardware and system resources.  
System calls are the only method through which a program can transition into kernel mode to perform privileged operations such as file I/O, memory management, and process control.

## How System Calls Work

When a user program requires a system-level operation:  
1. **Request**: The program issues a system call.  
2. **Mode Switch**: The OS switches from user mode to kernel mode.  
3. **Execution**: The kernel performs the requested task.  
4. **Return**: Control is passed back to the user program.  

This transition ensures system integrity and resource protection.

## Features

- **Interface**: System calls define a standardized API for user programs.  
- **Kernel Mode Access**: Grants controlled access to memory, devices, and CPU.  
- **Context Switching**: The system saves process state and switches to kernel code, which introduces slight overhead.

## Common Services

- **Process Control**: `fork()`, `exec()`, `exit()`  
- **File Operations**: `open()`, `read()`, `write()`, `close()`  
- **Device Management**: Request and release I/O access  
- **Memory Management**: Allocate and free runtime memory  
- **IPC**: Pipes, sockets, shared memory  
- **System Info**: Read or update system state

## Context Switching (Preview)

Each system call involves saving the process state, switching to kernel mode, executing the service, and restoring the process state.  
This ensures isolation but can impact performance if overused.

## References+Further learning

- [GeeksforGeeks: Introduction to System Calls](https://www.geeksforgeeks.org/operating-systems/introduction-of-system-call/)  
- [TutorialsPoint: System Calls in UNIX and Windows](https://www.tutorialspoint.com/system-calls-in-unix-and-windows)

## PC Optimization Sessions

For  PC optimization, latency reduction, and FPS tuning, join my Discord:  
[https://discord.gg/GXXrZzjYbt](https://discord.gg/GXXrZzjYbt)
