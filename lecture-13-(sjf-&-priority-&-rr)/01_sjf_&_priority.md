# 🧠 What Is CPU Scheduling Again?

It’s the **way the operating system decides** which process gets to use the CPU and for how long.

The goal is to:
- Use CPU efficiently,
- Keep things fast and responsive,
- Make sure every process gets its turn fairly.

## 🔹 1. **Shortest Job First (SJF) – Non-Preemptive**

### 📌 What is it?
- The **process with the smallest Burst Time (BT)** is picked first.
- Non-preemptive = Once a job starts, it **cannot be interrupted**.

### 🔍 a. **Least Burst Time Goes First**
- OS checks which process has the **smallest execution time** (BT) and gives it the CPU.

### ⚠️ b. **Problem: Burst Time Must Be Estimated**
- The OS must **guess** how long each process will take (BT), which is difficult in real life.
- Perfect estimation is **almost impossible**.

### 💡 c. **Choose the Job with Smallest Remaining Time**
- SJF picks the job that takes the **least time to complete** (currently available in the queue).
- In non-preemptive mode, once chosen, it **runs till it finishes**.

### 🚛 d. **Can Still Suffer from Convoy Effect**
- If a **long job comes first**, all small jobs **get stuck behind it**, leading to delays.


### 🛑 e. **Starvation Can Occur**
- Short jobs keep getting selected first.
- **Long jobs may never get a chance** if short jobs keep arriving.

### 🧾 f. **Selection Criteria**
- Arrival Time (AT) + Burst Time (BT)
- Pick the job with **smallest BT among all that have arrived**.


---

## 🔹 2. **Shortest Job First – Preemptive (Also called Shortest Remaining Time First)**

### 📌 What is it?
- **Preemptive = Can interrupt a running job** if a shorter one arrives.

### ✅ a. **Less Starvation**
- Since jobs can be interrupted, the system is more **flexible**.
- New short jobs **don’t have to wait for a long job to finish**.

### ✅ b. **No Convoy Effect**
- Long jobs can be **paused**, so short jobs **don’t get stuck behind** long ones.

### 🌟 c. **Why It’s Good: Lower Average Waiting Time**
> 📌 "Gives average WT less for a given set of processes as scheduling short job before a long one decreases the WT of short job more than it increases the WT of the long process."

Let’s simplify:
- Suppose a short job (needs 2 sec) comes while a long job (needs 10 sec) is running.
- If we finish the short one first:
  - The short job **waits less**.
  - The long job **waits a bit more**, but overall, it’s a **win** in total average waiting time.

---

## 🔸 3. **Priority Scheduling – Non-Preemptive**

### 📌 What is it?
- Every process is given a **priority** when it’s created.
- CPU picks the process with the **highest priority** (higher number = higher priority).

---

## ⚠️ Correction: Priority Number Meaning

In **some systems**, **higher number = higher priority** (e.g., priority 12 > priority 4).
In **other systems**, it's the opposite: **lower number = higher priority** (e.g., priority 1 > priority 5).

* So, **higher number = higher priority** in your case.
* Dont get confused

---

### 📘 a. **Assigned at Creation Time**
- Like giving students ranks: Process with **Rank 1 goes first**.

### 🔁 b. **SJF Is a Special Case of Priority Scheduling**
- If you use **Burst Time as a priority (shorter = higher)**, SJF becomes a form of priority scheduling.

---


## 🔸 4. **Priority Scheduling – Preemptive**

### 📌 What is it?
- A running process **can be interrupted** if a new process with **higher priority** arrives.

### 🚫 a. **Can Cause Starvation**
- Low-priority jobs may never run if high-priority jobs keep arriving.
- This means some jobs **wait forever**.

### ✅ Solution: **Aging**
> Gradually increase the priority of waiting jobs so they eventually run.

### 🧓 i. **What is Aging?**
- Let’s say a process has been waiting a long time.
- Its priority is **increased slowly over time**, so it eventually becomes high enough to run.
- Example: Increase priority every 15 minutes.

### ✅ ii. **Prevents Starvation**
- Ensures **all processes get their turn**.
- Makes the system **fair and efficient**.

## ✅ Why Do We Need These Scheduling Methods?

| Feature/Goal                      | Why It Matters                                                      |
|----------------------------------|----------------------------------------------------------------------|
| Efficient CPU use                | Don’t waste resources – make full use of CPU.                        |
| Shorter turnaround/wait times    | Make system **faster** and more **responsive** to users.             |
| Fairness                         | Prevent any process from being ignored forever.                     |
| Avoid Convoy Effect              | Prevent delays from one slow process blocking fast ones.            |
| Better system throughput         | Handle more tasks in less time.                                      |
| Suitable for different scenarios | Real-time apps, gaming, servers, etc., all need different strategies.|
