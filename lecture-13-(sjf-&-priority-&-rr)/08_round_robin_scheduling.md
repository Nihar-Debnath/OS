# 🧭 What is Round Robin (RR) Scheduling?

> Think of RR like a **turn-based game** or **queue in a bank**: everyone gets a fixed time to play/work, and if they don’t finish, they go back to the end of the line and wait for their turn again.

It is one of the **most popular and fair** scheduling algorithms.

### 🔹 5. Round Robin Scheduling (RR)

### 📌 a. **Most Popular**
- Widely used in **general-purpose operating systems** like Windows, Linux, etc.
- Loved for its **fairness** and **simplicity**.

### 📌 b. **Like FCFS but Preemptive**
- FCFS = First Come, First Serve.
- In FCFS, a process once started runs until it finishes.
- In RR, a process **runs for a fixed time**, then **goes back** to the queue if not finished.
- This makes RR **preemptive** – it **interrupts** processes and gives everyone a fair slice of CPU.

### 📌 c. **Made for Time-Sharing Systems**
- RR is **perfect for modern operating systems** where multiple users/programs share CPU time.
- Each process gets a **time quantum (TQ)** – a small fixed time slice (e.g., 100ms).
- Feels like all programs are running at once, even if CPU handles them one at a time.

### 📌 d. **Criteria = Arrival Time (AT) + Time Quantum (TQ)**
- Unlike SJF or Priority Scheduling, it **does NOT care** about the process’s **Burst Time (BT)**.
- Only Arrival Time and **TQ** matter.

### 📌 e. **Low Starvation, No Convoy Effect**
- **No process waits forever** because everyone gets a turn.
- No one process hogs the CPU.
- There’s **no convoy effect** like in FCFS, where a big job blocks smaller ones.

### 📌 f. **Easy to Implement**
- Logic is simple:
  - Keep a **queue**,
  - Give each process CPU for **TQ** time,
  - If not finished, put it **back in the queue**.

### 📌 g. **Context Switch Overhead**
- If **TQ is too small**, CPU keeps switching between processes frequently.

> 🧠 This switch is called a **context switch** – where the CPU saves one process’s state and loads another’s.

- More switches = more **overhead** = slower system.
- So, **TQ must be chosen wisely**: not too small, not too big.

## 🔁 🔄 Round Robin Flow (Explaining the Diagram)

Let’s break down the diagram step by step:

1. **Ready Queue**: List of processes waiting to run.

2. **Pick a Process (FCFS)**: First process in queue is selected.

3. **Check: Is Burst Time < Time Quantum?**
   - Yes ➝ Process is so short it can finish in one go.
     - So it's allowed to **run till completion**.
   - No ➝ Process needs more time.
     - It runs for **TQ only**, then...

4. **TQ Expires ➝ Check: Is Process Done?**
   - Yes ➝ Move to **Terminate State** (done).
   - No ➝ Put back in queue to wait for next round.

👉 This loop continues until **all processes are done**.

## ✅ Advantages of RR

| Feature                     | Benefit                                     |
|----------------------------|---------------------------------------------|
| Fairness                   | All processes treated equally                |
| Low starvation             | No process is left out                      |
| Fast response              | Ideal for interactive systems (like GUI apps) |
| Simple design              | Easy to code and understand                 |

## ❌ Disadvantages

| Problem                    | Reason                                  |
|---------------------------|-----------------------------------------|
| High overhead             | Too many context switches if TQ is small |
| Not ideal for long jobs   | Long jobs take multiple rounds to finish |
| Tuning TQ is tricky       | Too small = slow, too big = unfair       |

## 🛠️ Why Do We Need Round Robin?

- Operating systems often need to serve **multiple users and programs** at once.
- RR makes it feel like everything runs **simultaneously**, thanks to **frequent switches**.
- It ensures:
  - **No program is starved**
  - **Interactive apps respond quickly**
  - **System remains fair and predictable**