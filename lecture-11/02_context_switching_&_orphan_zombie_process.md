Let me break down each concept — **Context Switching**, **Orphan Process**, and **Zombie Process** — in a **very simple and beginner-friendly way**, line by line, and then I’ll also explain why each one is important.

## 🌀 2. Context Switching — When the CPU changes its focus!

### 🔍 What is it?

When the CPU stops working on one process and starts working on another, it needs to **pause and save the current process** and **load the next one**. This is called **context switching**.

### ✅ Explanation of each point:

#### a. *Switching the CPU to another process requires saving the current process’s state and restoring the next one.*

* Think of it like putting a **bookmark** in your current book and then opening another book to continue reading from where you left off.
* The **state of the process** (what it was doing, its data, etc.) is saved.

#### b. *The kernel saves the old process’s context in the PCB and loads the new one.*

* The **Process Control Block (PCB)** is like a report card that stores everything about a process.
* The kernel saves the old context into the PCB, and loads the new process’s context from its PCB.

#### c. *It is pure overhead — no useful work is done during context switching.*

* During switching, the CPU is not doing real work like running programs — it’s just **preparing to work**. That’s why it's called **overhead**.

#### d. *Speed depends on memory speed, number of registers, etc.*

* On faster systems with better memory and fewer things to save/load, switching is faster.

## 👶 3. Orphan Process — A child process left without a parent

### 🔍 What is it?

An **orphan process** is a child process whose **parent has died or finished** but the child process is still running.

### ✅ Explanation of each point:

#### a. *Parent process terminated, child is still running = orphan process.*

* Imagine a parent leaving the home while the child is still doing homework — now the child is “orphaned”.

#### b. *Init process adopts orphan processes.*

* The **init process** is like a **foster caretaker**. It adopts orphaned processes so the system stays stable.

#### c. *Init is the first process of OS.*

* It is always running and is the ancestor of all processes. In modern Linux systems, `systemd` is used instead of traditional `init`.

## 🧟 4. Zombie Process / Defunct Process — Dead, but still haunting

### 🔍 What is it?

A **zombie process** is a process that has **finished running**, but its **entry still exists in the process table**. It’s dead but not cleaned up.

### ✅ Explanation of each point:

#### a. *Zombie = execution done but still in process table.*

* It has completed its job but still **sits in memory** waiting for the parent to say, "Okay, I know you finished."

#### b. *Mostly happens with child processes — parent has to read exit status.*

* The **parent must check if the child finished** by calling a system function like `wait()`.
* Once the parent checks, the OS can remove it from the process table.

#### ➕ Bonus Terms:

* This checking and removing is called **reaping** the zombie.

#### c. *If parent takes too long to call wait(), zombie remains.*

* If the parent doesn’t call `wait()` soon, the child **lingers like a ghost**.

#### d. *Zombie stays until parent reads status (exit code).*

* Once the **exit status** is read, zombie is **fully cleaned up**.

## 🧠 Quick Summary (Memory Trick)

| Term               | What it means                                | Real-life analogy                           |
| ------------------ | -------------------------------------------- | ------------------------------------------- |
| **Context Switch** | CPU saves and switches to another task       | Bookmarking a book and reading another one  |
| **Orphan Process** | Child process continues after parent is gone | Child working after parent leaves           |
| **Zombie Process** | Process is done but not yet cleared          | Dead body not buried till paperwork is done |
