---
title: "Concurrency in Go, ch. 2"
date: 2024-05-26
---

# Concurrency in Go
_As I mentioned in a [previous post](./2024-05-26-booknotes-intro.md), I'm working on uploading some of my reading notes from [Concurrency in Go](https://amzn.to/3WXfxER). These are my unedited notes from chapter 2._

## Chapter 2

Chapter 2 is titled "Modeling your Code: Communicating Sequential Processes" and continues the overview of concurrent programming from [Chapter 1](./2024-05-26-concurrency-in-go-chapter-1.md). 

## Notes

Concurrently is a property of the code, parallelism is a property of the running program. Just because code is written to be executed concurrently doesn’t mean you will have parallel work being done. For example, a machine with only one core.

Go’s concurrency model (channels) is based on Tony Hoare’s paper: Communicating Sequential Processes (CSP). Introduced an IO approach to modeling concurrency, with a primitive similar to channels for message passing and synchronization. 

Since go’s runtime manages multiplexing and scheduling goroutines for you, you don’t have to worry about the lower level details of creating threads and scheduling them.

In go, there are lower level synchronization primitives such as mutexs etc. It’s generally preferable to use channels to synchronize IO, except when in performance critical sections.

Locks should generally be internal to a type and never exposed. 

Summary of the go philosophy on concurrency: aim for simplicity and readability, use channels when possible, and treat goroutines like a free resource. (Not sure I agree with the last point tbh).