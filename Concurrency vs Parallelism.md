# Concurrency vs Parallelism

## 🟦 Concurrent (Concurrency)

**Doing multiple tasks by _switching_ between them**

Concurrency is about **handling multiple tasks at the same time**, but **not necessarily executing them at the exact
same moment**.

- Tasks overlap in time
- Execution is interleaved
- Can work on a **single CPU core**
- Focuses on **responsiveness and structure**

Example:

- Switching between cooking and answering phone calls
- A web server handling many requests

---

## 🟩 Parallel (Parallelism)

**Doing multiple tasks at the _same time_**

Parallelism is about **executing multiple tasks at the exact same time**.

- Tasks run **simultaneously**
- Requires **multiple CPU cores**
- Focuses on **performance and speed**

Example:

👥 Two people cooking:

- One cooks rice 🍚
- One cooks curry 🍛

**In Computing**

- Data processing
- Image rendering
- Machine learning
- MapReduce

---

## 🔍 Key Differences

| Feature          | Concurrent     | Parallel                |
|------------------|----------------|-------------------------|
| Same time?       | ❌ Not exactly  | ✅ Yes                   |
| Execution time   | Overlapping    | Simultaneous            |
| CPU cores needed | 1 or more      | 2 or more               |
| Execution        | Interleaved    | Simultaneous            |
| Goal             | Responsiveness | Faster execution        |
| Nature           | Task switching | True parallel execution |

---

## Simple Analogy

- **Concurrency**: One person juggling multiple tasks by switching
- **Parallelism**: Multiple people doing tasks at the same time

---

## Programming Perspective

### Concurrency examples

- Async / Await
- Event loops
- Threads on a single core

### Parallelism examples

- Multiprocessing
- Parallel streams
- GPU / multi-core execution

---

### In Java

- Concurrency: `Thread`, `ExecutorService`
- Parallelism: `ForkJoinPool`, Parallel Streams

---

## Important Interview Line

> Concurrency is about **dealing with many tasks**  
> Parallelism is about **doing many tasks**

---

**How many threads can we create on a Machine?**

It depends on two things,

- **Core's** of the CPU.
- Amount of **RAM**.

**Virtual Threads ?**

Virtual Threads are super lightweight threads.

> **Threads** - Provided by Operating System.  
> **Virtual Threads** - Provided by JVM.  