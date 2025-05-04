Let’s break down **Lecture 12: Intro to Process Scheduling** into a very detailed, beginner-friendly explanation. We'll explain what it is, why we need it, and walk through each point clearly.

## 🧠 What is Process Scheduling?
Before diving into the specific points, let’s understand what process scheduling means and **why it's important**:

### Imagine:
You’re using a computer to do multiple things—watch YouTube, write notes, chat on WhatsApp Web, and run antivirus scans—all at the same time. But your **CPU (Central Processing Unit)** can only work on **one task at a time**.

So, how does it manage to handle everything so smoothly?

That’s where **process scheduling** comes in!

> 📌 **Process Scheduling** is the method used by the **Operating System (OS)** to decide **which task (or process)** should use the **CPU next** and for **how long**.

Without scheduling:
- Some tasks may **never get a turn** (starvation),
- The computer might become **slow or unresponsive**,
- And the **CPU might sit idle**, wasting power and time.

## 🔍 Detailed Explanation of Each Section:

### **1. Process Scheduling**
This is the foundation of multi-tasking in any computer.

#### a. **Basis of Multi-programming OS**
- In a **multi-programming OS**, multiple programs are loaded in memory.
- But since the **CPU can only run one process at a time**, it switches rapidly between them.
- **Scheduling** is what allows this switching in an efficient way.

#### b. **Switching CPU among processes makes computer more productive**
- If one process is doing nothing (like waiting for user input), the CPU can work on another task.
- This switching keeps the CPU **busy and efficient** rather than wasting time.

#### c. **Quantum and switching (Time-sharing concept)**
- **Time Quantum** is like a small time slice given to each process (say, 100 milliseconds).
- When a process’s time quantum ends, the OS **takes the CPU away** from it and **gives it to another process**.
- This keeps repeating in a cycle so every process gets a fair chance.
  
🟢 **Why it matters**: Without this, one big program could block everything else!

### **2. CPU Scheduler**
This is like the **manager** in charge of choosing who gets to use the CPU.

#### a. **When CPU becomes idle, pick a process from the ready queue**
- There’s a **queue** of processes waiting to be run.
- When the CPU becomes free, the scheduler selects the **next process** to run.

#### b. **Done by STS (Short Term Scheduler)**
- There are different types of schedulers:
  - **Short-Term Scheduler (STS)** chooses which ready process should run **next**.
  - It works **frequently** and must be **fast**, as it runs often.

🟢 **Why it matters**: It keeps the CPU busy and ensures smooth operation by managing who runs next.

### **3. Non-Preemptive Scheduling**
Once a process starts using the CPU, it **keeps it until it finishes or waits**.

#### a. **CPU not taken away once given**
- Imagine someone talking on the phone and won’t let go until they finish the call.
- In **non-preemptive scheduling**, once a process starts, it **can’t be stopped** until it’s done or voluntarily pauses.

#### b. **Starvation risk**
- A process with a **very long task** can keep the CPU for a long time.
- Other smaller, quick processes may **have to wait a lot**, even if they could finish in a second.
- This is called **starvation**.

#### c. **Low CPU Utilization**
- If the running process **is not using CPU actively** (maybe it's waiting for input), CPU **sits idle**, which is **inefficient**.

🟠 **Why it's less preferred**: Not ideal for modern systems where fairness and responsiveness are needed.

### **4. Preemptive Scheduling**
This is more common and smarter for multitasking systems.

#### a. **CPU is taken after time expires (or switch to wait/terminate)**
- Each process gets a **time quantum**.
- If it doesn’t finish in that time, it’s **paused**, and the CPU is **given to another process**.
- Also, if it switches to waiting/terminated state, CPU is re-assigned.

#### b. **Less Starvation**
- Because every process gets a fair **time slot**, even small and quick ones don’t have to wait forever.
- It’s more **fair and balanced**.

#### c. **High CPU Utilization**
- CPU is **always working**, switching between processes and never wasting time.
- This leads to better **overall performance**.

🟢 **Why it's better**: Most modern OS (like Windows, Linux, macOS) use **preemptive scheduling** for multitasking.

## ✅ Summary Table

| Feature                     | Non-Preemptive              | Preemptive                        |
|----------------------------|-----------------------------|----------------------------------|
| CPU given until process finishes | ✅ Yes                      | ❌ No (can be taken anytime)     |
| Starvation possible?       | ❗ Yes (long tasks block others) | ❌ Less likely                   |
| CPU Utilization            | 🔻 Low                      | 🔺 High                          |
| Used in modern OS?         | ❌ Rarely                    | ✅ Mostly used                  |
| Fairness                   | ❌ Less fair                 | ✅ More fair                    |

## 🧠 Why Do We Need Process Scheduling?

We need process scheduling to:
1. **Maximize CPU usage** — keep the CPU busy all the time.
2. **Ensure fairness** — every task gets a chance.
3. **Improve system responsiveness** — quick tasks don’t wait forever.
4. **Support multitasking** — allow many apps to run "at once".
5. **Avoid starvation and deadlocks** — prevent system freeze or unfairness.
