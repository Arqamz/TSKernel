# TSKernel - A Browser-Based Kernel Simulation with CLI Shell

**TSKernel** is a  project aimed at simulating an operating system in the browser. Instead of building a custom language and compiler right away, the initial focus will be on implementing a basic **kernel** that runs **processes** in the form of **CLI shell commands** or **shell scripts**. These commands will be mapped directly to kernel **system calls**, enabling users to interact with the kernel and test out various OS-like behaviors, such as process scheduling, memory management, and basic resource allocation.

This project aims to simulate the core aspects of an OS, with each "process" being a command or a script executed by the kernel, allowing for real-time process management and interaction.

---

## Table of Contents

1. [Overview](#overview)
2. [Key Features](#key-features)
3. [Core Components](#core-components)
4. [How It Works](#how-it-works)
5. [Development Goals](#development-goals)
6. [Installation & Setup](#installation--setup)
7. [FAQs](#faqs)

---

## Overview

**TSKernel** simulates a lightweight operating system within the browser that can **execute commands** or **shell scripts**. These scripts will invoke kernel **system calls** to interact with the environment, such as spawning new processes, allocating memory, and manipulating resources like files or the terminal window. The system will be **process-driven**: every process will be a shell command or a sequence of system calls that the kernel interprets and executes.

The goal is to emulate basic OS functionality, such as:
- **Process Scheduling**: Managing the execution order of processes using a simple scheduler.
- **Memory Management**: Allocating resources (memory, CPU time) to processes and ensuring processes do not interfere with each other.
- **Process Isolation**: Ensuring that processes cannot read/write to each other's memory.
- **System Calls**: Enabling processes to request kernel-level operations, like creating new processes or interacting with the file system.
- **Command-Line Interface**: Allowing users to interact with the kernel using a simple shell-like interface.

---

## Key Features

### Minimum Viable Kernel (MVP)
The MVP will focus on the following basic features:
- **Process Scheduling**: Basic management of processes, ensuring they are allocated CPU time in a fair or predefined manner (e.g., round-robin).
- **Memory Allocation**: Allocating memory to each process, ensuring each has its own isolated space.
- **CLI Shell**: A command-line interface that allows users to enter commands or shell scripts, which are translated into kernel system calls.
- **System Calls**: A set of basic system calls that interact with the browser environment (e.g., accessing the file system, spawning processes, reading input).
- **Process Isolation**: Ensuring that each process runs in its own isolated environment to prevent one process from accessing or modifying another's memory.

### CLI Shell & Process Execution
- **CLI Shell**: The user will interact with the kernel through a terminal-like interface, where they can issue commands or run simple scripts. These commands will translate directly into system calls executed by the kernel.
- **Shell Commands as Processes**: Instead of building a custom language, processes will be **shell commands or scripts** that invoke kernel operations. Each command will be a process in the kernel's process table, and the kernel will manage the execution of these commands.

### Kernel Interactions
- **Scheduling**: Each command/script is executed as a process in a scheduler, which determines when and for how long each process runs.
- **Memory Management**: Each process will be allocated a fixed amount of memory, with limitations to prevent one process from consuming all available resources.
- **Resource Management**: System calls for file management, process creation, and other kernel-level tasks will be made available to shell commands.

---

## Core Components

### Kernel
The kernel will manage the following:
- **Process Control**: Creating, running, and terminating processes. Each process will correspond to a shell command or script that interacts with the kernel.
- **Scheduling**: Managing multiple processes by allocating CPU time and ensuring they execute in a reasonable order.
- **System Calls**: Enabling processes to request access to system-level resources like file management or terminal manipulation.

### CLI Shell
The shell will serve as the **user interface** for interacting with the kernel. Users can:
- **Execute Commands**: Write basic shell commands or scripts that interact with the kernel.
- **Create Processes**: Each command or script will be a new process in the kernel, which will be scheduled and executed based on the kernel’s process management system.

### System Calls
The kernel will provide basic system calls for:
- **Creating Processes**: Creating new processes in the kernel.
- **Managing Files**: Reading/writing files via browser APIs like IndexedDB or the File System Access API.
- **Resource Management**: Allocating memory and CPU time to processes.

---

## How It Works

1. **Writing Shell Commands**: The user writes shell commands or scripts, which are interpreted by the shell.
2. **Translating to System Calls**: The shell commands are translated into **system calls** that the kernel can execute (e.g., creating a new process, reading a file).
3. **Process Execution**: The kernel schedules the processes, allocating resources like memory and CPU time.
4. **Managing Processes**: The kernel manages the lifecycle of each process, ensuring that they are properly scheduled, isolated, and terminated when they finish.

---

## Development Goals

### Minimum Viable Product (MVP)
- **Basic Kernel**: Implement a minimal kernel with process scheduling, memory management, and system calls.
- **CLI Shell**: Create a command-line interface that allows users to input shell commands and interact with the kernel.
- **Process Execution**: Enable processes (shell commands/scripts) to be scheduled and executed by the kernel.
- **Resource Allocation**: Ensure processes are allocated fixed CPU time and memory to prevent one process from overusing resources.

### Future Features & Ideas (Modular Extensions)
- **Advanced Scheduling**: Implement more advanced scheduling algorithms (e.g., priority-based scheduling).
- **File System Expansion**: Expand file management functionality with the File System Access API or IndexedDB.
- **Networking**: Allow processes to communicate over the network (using WebSockets or Fetch API).
- **GUI**: Introduce a graphical interface for interacting with the kernel.
- **Security Enhancements**: Implement stronger sandboxing and security measures to prevent process interference and memory corruption.

---

## Installation & Setup

To run the project locally:

1. Clone the repository:
   ```bash
   git clone https://github.com/arqamz/TSKernel.git
   cd TSKernel
   ```

2. Install dependencies (if any):
   ```bash
   npm install
   ```

3. Open `index.html` in your browser to start interacting with the kernel.

---

## FAQs

**Q1: How does this kernel interact with the actual browser environment?**  
The kernel runs in a JavaScript environment inside the browser, using the browser's APIs (such as File System Access API, IndexedDB, etc.) to simulate OS-like functionality. It interacts with the environment by interpreting and executing system calls triggered by user shell commands.

**Q2: What commands can I run in the shell?**  
The initial shell will support basic commands like `create_process()`, `read_file()`, `write_file()`, and system-level operations like `ls` (list processes), `ps` (process status), or simple arithmetic operations in scripts.

**Q3: Can I write custom scripts for the kernel?**  
Yes, the kernel will allow you to write custom shell scripts that interact with the system via system calls, effectively creating and managing processes within the browser environment.

**Q4: How does the kernel manage processes and resources?**  
The kernel will use a basic **round-robin scheduling algorithm** (or a more advanced option later) to allocate CPU time and memory to processes. It will enforce limits on resources to ensure that one process cannot monopolize the system.
