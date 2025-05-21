## 🧠 Why do we need CPU scheduling at all?

In a computer, the **CPU is like the brain** – it does all the thinking. But only **one process (task)** can use the CPU at a time. So we need a system to decide:

* Who gets to use the CPU next?
* For how long?
* What happens if a task is too slow?

This system is called a **CPU scheduling algorithm**. There are many types of them – some simple, some complex. One advanced and very **flexible** type is called:

## 🔁 **Multi-Level Feedback Queue (MLFQ)** – Explained Simply

Think of MLFQ as a **school with multiple classrooms (queues)**. Each classroom is for students with different needs:

* Fast learners in high-priority rooms
* Slower learners in lower-priority rooms

Here’s the breakdown from the image and your content:

### 📌 MLFQ Features (from your image):

#### a. **Multiple Sub-Queues**

* There isn't just one waiting line.
* There are **many levels of queues**.
* Each level has **different priority** and rules.

#### b. **Processes can move between queues**

* If a process **takes too long** (like a student needing more time), it is **moved to a lower-priority queue**.
* If a process is **quick and interactive** (like a student answering questions fast), it stays in or moves up to a **higher-priority queue**.
* This way, the CPU **focuses more on shorter and interactive tasks**.

📝 **BT = Burst Time** = how long a process needs the CPU.

➡️ Example:

* A game (interactive) would stay in a higher queue.
* A large file compression (long CPU time) would move to a lower queue.

#### ➕ Extra Benefit: **Ageing**

* If a process is stuck too long in a low queue, it may be moved up to avoid **starvation** (waiting forever).

#### c. **Less starvation than MLQ (Multi-Level Queue)**

* In MLQ, once you’re in a queue, you’re stuck. But in MLFQ, you can move!
* So **MLFQ is smarter and fairer**.

#### d. **Flexible**

* You can design MLFQ to behave differently depending on your system’s needs.

#### e. **Customizable**

* You can set how many queues, what time quantum (how long a process gets the CPU), and how ageing works.

## 🧱 Example MLFQ Design (based on image)

This example uses **4 levels** of queues:

| Queue Level | Priority | Scheduling Type      | Time Quantum |
| ----------- | -------- | -------------------- | ------------ |
| Queue 1     | Highest  | Round Robin          | 2 ms         |
| Queue 2     | Medium   | Round Robin          | 4 ms         |
| Queue 3     | Low      | Round Robin          | 8 ms         |
| Queue 4     | Lowest   | FCFS (no time limit) | ∞            |

🔄 **Flow**:

* All new processes start at Queue 1.
* If a process uses up its time (2ms), it moves to Queue 2, and so on.
* If it waits too long, it may be moved back up (ageing).
