# Multithreading

## Resource:

[🧵 Concurrency & Multithreading COMPLETE Crash Course | All you need to know for any LLD Rounds ‼️](https://youtu.be/Rot2QnaUqBU)

## 🔹 Concurrency vs Parallelism

* **Concurrency** → Multiple tasks in progress (not necessarily same time)
* **Parallelism** → Tasks running exactly at same time

> Parallelism - Human can **Speak and Walk** parallelly.</br>
> Concurrency - Human can **Drink water then Speak**, either one at a time. (Task switching)

## Threads 🧵

* Thread → **the smallest units of execution.**
* Enables:
	* ⚡ Concurrency
	* 🚀 Better CPU utilization
	* 🖥️ Parallel execution (on multicore systems)

> ✅ In a **4 core CPU**, 4 threads can run in **parallel**, but you can create **N threads** (OS schedules them).

## 📘 Process vs Threads

| Characteristics        | Process                                                  | Thread                                                       |
|------------------------|----------------------------------------------------------|--------------------------------------------------------------|
| 📋 Definition          | An **independent program** with its **own memory space** | A lightweight **unit of execution within a process**         |
| 🧠 Memory              | **Separate** memory space                                | **Shared** memory within a same process                      |
| 🧰 Resource Allocation | **Fully independent** resource allocation.               | **Shares resources** with other threads in the same process. |
| ⚖️ Overhead            | High (creating a new process is resource-intensive)      | Low (Threads are lightweight and quick to create)            |

## 📘 Thread vs Runnable vs Callable

### 🔹**Thread**

* Direct access to Thread methods
* Cannot extend another class❌
* Each task requires a new Thread instance.

### 🔹**Runnable**

* **Return type**: `void run();`
* Cannot throw checked exception❌

### 🔹**Callable**

* The `Callable` interface, introduced in **Java 5** as part of **concurrency utilities**, provides a more powerful
  alternative to `Runnable`.</br>
* **Return type**: `V call() throws Exception;` it can `throws` **checked exception❌**
* `Callable` works with `Future` objects to **retrieve results** after task completion.

---

### 🛠️ How `Callable` works ?

It works only with the `ExecutorService` framework rather than directly extending `Thread`.

**Example:-**
<!-- @formatter:off -->
```java
ExecutorService ex = Executors.newSingleThreadExecutor();
Future<Integer> result = ex.submit(() -> 10);
System.out.println(result.get());
```
<!-- @formatter:on -->

## QA?

### 1️⃣ What is Thread safety and how can it be achieved ?

**Thread safety** means _multiple threads_ can access shared data without issues.</br>

**✅How to achieve:**

* `synchronized`
* `ReentrantLock`
* `volatile`
* `Atomic classes` (e.g., AtomicInteger)
* `Concurrent collections`
* `Immutable objects`

### 2️⃣ `start()` vs `run()` method ?

* `start()` method **begins thread execution** and calls the `run()` method.
* `run()` method simply contains the code to be executed.

> ⚠️ Directly calling `run()` **won't create new thread**, it will execute in main thread.🔁

### 3️⃣ `sleep()` vs `wait()` method ?

### 🛌 `sleep()`

* Belongs to: **Thread** class
* It causes the current thread to **pause for specific time** without releasing Lock🔒.

```java
synchronized void sleepExample() {
	Thread.sleep(5000); // won't release 🔒Lock until it got complete.
}
```

### ⏳ `wait()`

* Belongs to: **Object** class
* Must be inside synchronized block
* It causes the current thread to **wait until another thread invokes** by using `notify()` or `notifyAll()` method on
  the same
  object, and it **releases the lock** on the object.

	* 1️⃣ When a thread calls `wait()`, it **releases the 🔓 lock on the synchronized object** it was holding.
	* 2️⃣ Other threads can now acquire the lock and continue execution🔁.
	* 3️⃣ The waiting thread remains **idle** until another thread call `notify()` or `notifyAll()`.

```java
synchronized void waitExample() {
	object.wait();
}
```

### 4️⃣ `notify()` vs `notifyAll()` method ?

* `notify()` will resume only **one thread** which are in wait state.
* `notifyAll()` will resume **multiple threads** which are in wait state.

| Method        | Behavior                      |
|---------------|-------------------------------|
| `notify()`    | Wakes **one thread**          |
| `notifyAll()` | Wakes **all waiting threads** |

## 🏊 Thread Pools in Java.

* **Thread pools** are a managed collection of **reusable threads** designed to execute tasks
concurrently.
* They offer significant advantages in **resource management**, **performance**, and **application stability**.