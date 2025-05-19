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

