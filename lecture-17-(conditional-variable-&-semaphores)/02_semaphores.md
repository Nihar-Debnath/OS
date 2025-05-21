## 🚦 What is a Semaphore?

A **Semaphore** is like a **counter** that controls how many threads (workers) can access a **shared resource** (like a printer, room, or machine) at the same time.

---

## 🔢 How does it work?

* Imagine you have **3 washing machines** and many people want to wash clothes.
* You give out **3 tokens** (Semaphore = 3).
* Only people with a token can use a machine.
* Once someone finishes washing, they return the token — now someone else can use it.

This is exactly how a **counting semaphore** works!

---

## 📚 Key Points Explained Simply:

### a. Synchronization method:

* Semaphore is used to **coordinate** threads so they don’t mess up shared things.

### b. It uses a number (integer):

* That number tells **how many resources** are available.

### c. Multiple threads can use resources **at the same time**, if allowed.

### d. Semaphore vs Mutex:

* **Semaphore**: Controls access to **many resources**.
* **Mutex**: Controls access to **just one resource** at a time.

---

## 🧨 Types of Semaphores:

### 🔘 e. Binary Semaphore (0 or 1)

* Like a **Yes/No** switch.
* Only **1 thread** can use the resource at a time (like a mutex).

### 🔢 f. Counting Semaphore (0 to ∞)

* You can set it to any number like 2, 3, 10, etc.
* Useful when you have **multiple identical resources**.

---

## 🔄 Avoiding Busy Waiting

### g. Problem:

* Without smart logic, a thread may keep **checking again and again**: “Is the resource free yet?”

### ✅ Solution:

* If no resource is free, the thread will simply **go to sleep (block itself)** and **wait quietly**.

* When a resource becomes free, the thread is **woken up** and allowed to continue.

---

## 🔔 h. How does wake-up work?

* When a thread finishes its work and **returns the resource**, it sends a **signal**.
* That signal **wakes up one of the waiting threads**, and it gets its turn.

---

## 💡 Super Simple Example:

Let’s say:

* Semaphore = 2 (You have 2 printers).
* 5 people want to print documents.

Steps:

1. First 2 people get to print.
2. The next 3 people have to **wait**.
3. When one printer is free, a **signal** is sent to wake up **one waiting person**.
4. This repeats until all are done.


---
---
---

## 🧵 Example with Threads (Bottom of the Image)

Let’s simulate what happens with **3 threads (T1, T2, T3)** and **S(2)**:

### ➤ T1 does `wait()`:

* S = 2 → becomes 1
* T1 enters critical section ✅

### ➤ T2 does `wait()`:

* S = 1 → becomes 0
* T2 enters critical section ✅

### ➤ T3 does `wait()`:

* S = 0 → becomes -1 ❌
* Since value < 0, T3 is **blocked** and added to the block list 🚫

### When T1 or T2 finishes, they will call `signal()`, which will:

* Increase the value of S
* Wake up T3 if it’s in the block list

## 📌 Summary (Super Simple)

| Thread | Action | Semaphore Value | Result        |
| ------ | ------ | --------------- | ------------- |
| T1     | wait   | 2 → 1           | Enters ✅      |
| T2     | wait   | 1 → 0           | Enters ✅      |
| T3     | wait   | 0 → -1          | Blocked ❌     |
| T1     | signal | -1 → 0          | T3 wakes up ✅ |
