## 🛠️ 4. Solution to Race Condition

### a. **Atomic Operations**

* Atomic = **All or nothing**.
* These operations **cannot be interrupted** while executing.
* Done in **a single CPU step**, so no thread can "jump in" halfway.

🧠 Example:

In c++ we can create a atomic variable for **count++** like this:

```cpp
__atomic_add(&counter, 1);  // Atomic increment
```

Only one thread can change `counter` at a time.

---

### b. **Mutual Exclusion (Mutex) Using Locks**

* A lock is like a **"room key"** for the critical section.
* Only one thread can enter (run that part of code) if it **has the key (lock)**.
* Others have to **wait** outside.

🧠 Example (in C++):

In c++ **mutex** is used for locks

```cpp
#include <mutex>
mutex m;

void critical_section() {
    m.lock();   // Take the key
    // Work with shared data
    m.unlock(); // Return the key
}
```

---

### c. What is a Semaphore?

A **semaphore** is a synchronization tool used to control access to a shared resource in concurrent programming (like multiple threads or processes).

* Think of it like a **traffic signal or a ticket system** that regulates how many threads can enter a critical section (CS) or access a resource at a time.
* Semaphores help **avoid race conditions** by ensuring that only a limited number of threads can execute a piece of code simultaneously.


### Types of Semaphores:

1. **Binary Semaphore (Mutex):**

   * Can only be 0 or 1.
   * It works like a lock:

     * If the semaphore is 1 (unlocked), a thread can enter the CS and sets it to 0 (locked).
     * When leaving the CS, the thread sets it back to 1 (unlocked).
   * Only one thread can enter the critical section at a time.

2. **Counting Semaphore:**

   * Holds a count representing the number of available resources or permits.
   * Threads decrement the count to enter, and increment it when they leave.


### How does a Semaphore solve race condition?

Using a **binary semaphore (mutex)**, threads must **wait** before entering the critical section if another thread is already inside. This **serializes access** to the critical section, preventing simultaneous updates that cause race conditions.

* When a thread wants to enter the CS, it does a **wait (P operation)** on the semaphore:

  * If the semaphore is 1, it becomes 0, and the thread enters the CS.
  * If it is 0, the thread waits (blocks) until the semaphore becomes 1 again.
* When leaving the CS, the thread does a **signal (V operation)**:

  * The semaphore is set back to 1, allowing another waiting thread to enter.


### Quick example of binary semaphore usage (pseudo-code):

```c
semaphore mutex = 1;

Thread() {
  wait(mutex);    // Request access (if mutex=1, continue; else wait)
  // Critical Section - only one thread allowed here at a time
  signal(mutex);  // Release access (mutex=1, allow others in)
}
```

---

### What is **Bounded Waiting** in Critical Section?

**Bounded waiting** means:

> There is a **limit on the number of times other threads can enter their critical sections** after a thread has requested to enter and before it gets the chance to enter.

In simpler terms:

* Suppose Thread A wants to enter the critical section.
* Bounded waiting guarantees that Thread A **won't wait forever** while other threads keep cutting in line.
* There's a maximum number of times other threads can jump ahead before Thread A is allowed in.

---

### Why is Bounded Waiting Important?

* Without bounded waiting, a thread can be **starved** (never get to enter its critical section).
* Bounded waiting ensures **fairness** — no thread waits indefinitely.

---
---

## ❌ 5. Can a simple flag (like a boolean variable) solve race condition?

**No.**
Because:

* Flags themselves are shared data.
* Without proper control, **both threads can still enter at the same time** before the flag is updated properly.

### What is a simple flag here?

Imagine you have a shared boolean variable:

```c
bool flag = false;
```

And you try to use it like this to control access to a critical section:

```c
if (!flag) {
    flag = true;   // Indicate critical section is occupied
    // critical section code here
    flag = false;  // Leave critical section
}
```

### Why can’t this simple flag prevent race conditions?

The main reason is that **reading and writing the flag are not atomic and can be interleaved in problematic ways**. Let’s see an example.

### Problem example with two threads (Thread A and Thread B):

1. Both threads check `if (!flag)` at about the same time.

   * Since `flag` is initially `false`, **both see it as false** (meaning the CS is free).

2. Both threads enter the `if` block because the condition is true for both.

3. Thread A sets `flag = true` indicating it's in the critical section.
   Meanwhile, Thread B **hasn't updated the flag yet**, so it still thinks it's safe to enter.

4. Now **both Thread A and Thread B execute the critical section simultaneously**, causing race condition and data corruption.

### Why does this happen?

Because:

* The `if (!flag)` check and `flag = true` assignment are **two separate operations**, and there is **no guarantee they execute atomically** (all at once).
* Between the check and the set, **another thread can intervene** and also pass the check before the first thread sets the flag.
* This creates a **time window** where both threads think they have exclusive access, but actually don't.

### What’s missing here?

* There is **no synchronization or atomicity** to prevent the interleaving.
* A proper solution requires **atomic operations** or **locks/semaphores** that make the "check-and-set" action indivisible.

---
---
---

## ✅ 6. Peterson's Solution (for 2 threads only)

This is a **classic algorithm** that:

* Lets **two threads** take turns.
* Ensures **only one** is in the critical section at a time.

🧠 Very basic logic:

* Each thread says "I want to go!"
* But also says, "Let the other one go first if it's their turn."


---

**Peterson’s Solution** is a classic software-based algorithm that solves the **mutual exclusion problem** for **two processes (or threads)** without using hardware atomic instructions or semaphores. It guarantees:

* Mutual exclusion (only one thread in critical section at a time)
* Progress (no deadlock)
* Bounded waiting (no starvation)

## How Peterson’s Solution works and how it solves the race condition issue:

It uses **two shared variables:**

* `flag[2]` — an array of booleans to indicate if a process wants to enter the critical section.
* `turn` — an integer indicating whose turn it is to enter the critical section.

### Algorithm for two processes (Process 0 and Process 1):

Each process executes this before entering the critical section:

```c
flag[i] = true;          // Process i wants to enter critical section
turn = j;                // Give turn to the other process j
while (flag[j] == true && turn == j) {
    // Busy wait (do nothing) until the other process is not interested
}
```

After this wait finishes, Process `i` enters the critical section safely.

When done:

```c
flag[i] = false;         // Process i is leaving critical section
```

### Why does this solve the race condition?

1. **Mutual exclusion**:

   * Both processes can’t be in the critical section simultaneously.
   * If both want to enter, the `turn` variable gives priority to one process, forcing the other to wait.

2. **Progress**:

   * If one process is not interested (`flag[j] == false`), the other enters immediately.
   * So processes don’t wait unnecessarily.

3. **Bounded waiting**:

   * Because `turn` alternates and each process eventually gets its turn, no process waits forever.

### Step-by-step example:

* Suppose Process 0 wants to enter CS:

  * It sets `flag[0] = true`.
  * Sets `turn = 1` (gives turn to Process 1).
  * Checks if Process 1 wants to enter (`flag[1] == true`) and if it’s Process 1’s turn (`turn == 1`).
  * If Process 1 doesn’t want to enter or it’s not Process 1’s turn, Process 0 proceeds.

* If both try at the same time, `turn` decides who goes first, and the other waits.

### Why can't this be broken by context switches?

Because the **check and decision** (`while (flag[j] && turn == j)`) is inside a loop that keeps checking the condition until the other process backs off.

* The `turn` variable ensures **one process defers to the other** if both want to enter at once.
* The `flag` array ensures both processes **express interest** clearly.


### Visual analogy:

* Two friends want to enter a room.
* Both raise their hands (`flag[i] = true`) saying they want to enter.
* They decide who goes first by `turn`.
* The one whose turn it is enters while the other waits.
* After the first leaves, it lowers their hand (`flag[i] = false`), allowing the other in.


## But remember one thing Petersion solution also have problem that it only used for 2 threads max, we cant use it for more threads

- Not used much in real-world now, but good for **theory and understanding**.

---
---
---
---

## 🔒 7. Mutex/Locks — Advantages & Disadvantages

### ✔️ Why Use:

* Ensures **only one thread** accesses critical section → No race condition

### ❌ Disadvantages:

| Problem        | Meaning                                                                        |
| -------------- | ------------------------------------------------------------------------------ |
| **Contention** | Too many threads are waiting for the lock → performance drop                   |
| **Deadlock**   | Two threads wait on each other’s lock → Both freeze forever                    |
| **Debugging**  | Hard to find bugs when threads are stuck                                       |
| **Starvation** | Low-priority thread keeps getting ignored if high-priority threads keep coming |

---
---
---

Would you like a real-life **story analogy** to help lock and race condition make more sense?

## 🍩 The Donut Shop Analogy (Story)

### Characters:

* **Alice** and **Bob** are two co-workers.
* They share a **common fridge** at the office that sometimes has **exactly one donut** inside.
* They both love donuts. If there's a donut in the fridge, they want to eat it.


### The Race Condition (No Lock)

One morning, a donut is placed in the fridge. Alice and Bob both walk toward the fridge **at the same time**.

Here’s what happens:

1. **Alice opens the fridge and sees the donut.**
2. **Bob also opens the fridge and sees the donut.**
3. Both think: “Yum! I’m going to take it.”
4. Alice and Bob both reach for the donut.
5. 💥 **They grab the same donut at the same time.**
6. The donut is squished or both think they took it — **confusion and a ruined snack**.

This is a **race condition** — both tried to use a shared resource (the donut) at the same time **without coordination**.

### Adding a Lock (A Key System 🔑)

To prevent donut disasters, the office installs a **lockable fridge door** and gives **one key** to be shared.

Here’s the new rule:

* If you want a donut, you **must take the key** before opening the fridge.
* If someone else has the key, you **wait until they return it**.

### What happens now:

1. Alice and Bob both go for the fridge.
2. Alice gets the key first.
3. Bob sees Alice has the key and **waits**.
4. Alice checks the fridge, finds the donut, eats it, and returns the key.
5. Bob takes the key, opens the fridge — but the donut is gone.
6. No confusion, no squished donuts.

This is how **a lock (or mutex)** works — only one person can **enter the critical section (the fridge)** at a time.

---

### Mapping the analogy to real computing concepts:

| Real Life                    | Computer Concept            |
| ---------------------------- | --------------------------- |
| The fridge                   | Shared resource / memory    |
| The donut                    | Shared data (e.g., counter) |
| Alice & Bob                  | Threads or processes        |
| Both grabbing the donut      | Race condition              |
| The key to the fridge        | Lock / Mutex                |
| Waiting for the key          | Blocking or busy waiting    |
| Only one person using fridge | Mutual exclusion            |

### Bonus: What if there’s **no key and a sticky note instead**?

Imagine they use a note like:

> "Hey, I’m checking the fridge — please wait! – Alice"

This is like using a **flag variable**. But if Bob comes in **before Alice posts the note**, he doesn't know she’s about to enter, and they might **both enter at once** — just like how a boolean flag fails to prevent race conditions if it's not atomic.

### Conclusion

* **Race conditions** happen when multiple "people" (threads) try to grab the same thing at once without coordination.
* **Locks** are tools (like a key) that ensure only one can enter at a time.
* **Without locks**, things get messy and unpredictable.
* **With proper locking**, everything is orderly — even if you don’t get the donut 😄.