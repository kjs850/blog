---
title: process and thread
---
date: 2018-12-05 11:03:07

## Process

A Process is a program in execution. 
It has its own address space, a call stack, and link to any resources such as open files.
A computer system normally has multiple processes running at a time. 
The operating system keeps track of all these processes and facilitates their execution by sharing the processing time of the CPU among them.

## Thread

A thread is a path of execution within a process. 
Every process has at least one thread - called the main thread. The main thread can create additional threads within the process.
Threads within a process share the process’s resources including memory and open files. 
However, every thread has its own call stack.
Since threads share the same address space of the process, creating new threads and communicating between them is more efficient.


## reference
https://www.callicoder.com/java-concurrency-multithreading-basics/#processes-and-threads

categories:
- java

tags: 
- process
- thread

