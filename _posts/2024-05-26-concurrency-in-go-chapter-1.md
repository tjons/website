---
title: "Concurrency in Go, ch. 1"
date: 2024-05-25
---

# Concurrency in Go
_As I mentioned in my [previous post](./2024-05-26-booknotes-intro.md), I'm working on uploading some of my reading notes from [Concurrency in Go](https://amzn.to/3WXfxER). These are my unedited notes from chapter 1._

## Chapter 1

Chapter 1 is titled _An Introduction to Concurrency_, and focuses on discussing some of the background theory and principles behind concurrent programming.

## Definitions
**Concurrent**: a process that occurs simultaneously with one or more processes

**Embarrassingly** parallel: a problem that can easily be divided into parallel tasks
Embarrassingly parallel problems should be solved in a way that the program can scale horizontally.

**Horizontal scaling**: can take instances of your program, run it on more CPUs, or machines, and this will cause the runtime of the program to improve

**Race condition**: occurs when two or more operations must execute in the correct order, but the program has not been written in such a way to guarantee that this order is maintained.

**Data race**: one concurrent operation attempts to read a piece of data while another concurrent operation is attempting to write to the same variable

**Atomicity**
Something that is considered atomic has the property that within the context that it is operating, it is indivisible or uninterruptible. Key part here is context - something may be atomic in one context but not another.
Eg, something atomic with the context of the process may not be atomic within the context of the OS, or something that is atomic within the context of the OS may not be atomic within the context of the machine, operation that is atomic within the context of the machine may not be atomic within the context of the application. Layers of atomicity. Can change depending on the currently defined scope. Combining atomic operations does not necessarily produce a larger atomic operation.
Why does atomicity matter? If something is atomic, it is implied that it is safe within concurrent contexts.

**Critical section**: a section of a program that needs exclusive access to a shared resource

**Deadlock**: a deadlocked program is one in which all concurrent processes are waiting on one another

**Coffman Conditions**:
1. Mutual Exclusion: a concurrent process holds exclusive rights to a resource at any one time
2. Wait for Condition: a concurrent process must simultaneously hold a resource and be waiting for an additional resource
3. No Preemption: a resource held by a concurrent process can only be released by that process, so it fulfills this condition.
4. Circular Wait: a concurrent process (P1) must be waiting on a chain of other concurrent processes (P2), which are in turn waiting on it (P1), so it fulfills this final condition
If you can disprove any one of the 4 Coffman Conditions, you can prevent deadlocks.

**Livelock**: programs that are actively performing concurrent operations, but these operations do nothing to move the state of the program forward
Two or more concurrent processes attempting to prevent a deadlock without coordination often is a cause of a livelock.
Think of two people trying to walk down the sidewalk and each stepping in front of the other to go around each other and never going anywhere. That’s a livelock.

**Starvation**: any situation where a concurrent process cannot get all the resources it needs to perform work.
Starvation usually implies that there are one or more concurrent process that are greedy, i.e., unfairly preventing other concurrent processes from performing their work either as efficiently as possible or at all



