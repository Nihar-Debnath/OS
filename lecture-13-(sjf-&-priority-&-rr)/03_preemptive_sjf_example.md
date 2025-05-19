Let's solve the **Preemptive SJF (Shortest Job First)** algorithm, also known as **Shortest Remaining Time First (SRTF)**

---

## 🔧 **Given Data**

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P1      | 0                 | 8 - 1 = 7       |
| P2      | 1                 | 4               |
| P3      | 2                 | 9               |
| P4      | 3                 | 5               |

---

## ✅ Step-by-Step (Preemptive SJF / SRTF)

We will track the remaining burst times and schedule the process with the **shortest remaining time** at **each unit of time**.

---

### 🕒 Time 0:

* Only **P1** has arrived at AT 0.
* Run **P1** (P1 will run for 1 second because sjf will compare that any process even came after 1 seconds then it will find P2 who had arrived at time 1, so P1 will remain pause.)

### 🕒 Time 1:

* **P1** (initially 8 but ran for 1 so **8 - 1 =  7** left) and **P2** (4) have arrived.
* Shortest BT: **P2**
* Switch to **P2**

### 🕒 Time 1–5:

* Run **P2** continuously (has shortest BT)
* **P2** finishes at time **5** (Here sjf will completely finished the **P2** because after 2 seconds there is **P3** came but it has more BT then **P2**, and after 3 seconds also **P4** have BT more than **P2**)

### 🕒 Time 5:

* P3 (9), P4 (5), P1 (7 remaining) are in queue.
* Shortest: **P4**
* Run **P4**

### 🕒 Time 5–10:

* Run **P4** to completion
* **P4** finishes at time **10**

### 🕒 Time 10:

* Remaining: P1 (7 left), P3 (9)
* Shortest: **P1**
* Run **P1**

### 🕒 Time 10–17:

* Run **P1** (remaining 7) to completion
* **P1** finishes at time **17**

### 🕒 Time 17–26:

* Only **P3** remains (9 units)
* Run **P3**
* **P3** finishes at **26**

---

### 📊 Final Gantt Chart

```
| P1 | P2 | P4 | P1 | P3 |
0    1    5    10   17   26
```

---

## 📋 Final Table

| Process | AT | BT | CT | TAT = CT - AT | WT = TAT - BT |
| ------- | -- | -- | -- | ------------- | ------------- |
| P1      | 0  | 8  | 17 | 17            | 9             |
| P2      | 1  | 4  | 5  | 4             | 0             |
| P3      | 2  | 9  | 26 | 24            | 15            |
| P4      | 3  | 5  | 10 | 7             | 2             |

---

### 🔢 Averages

* **Average TAT** = (17 + 4 + 24 + 7) / 4 = **13 units**
* **Average WT** = (9 + 0 + 15 + 2) / 4 = **6.5 units**

---

## ⚖️ Preemptive vs Non-Preemptive SJF (Difference for This Case)

| Feature                    | Preemptive SJF (SRTF)         | Non-Preemptive SJF            |
| -------------------------- | ----------------------------- | ----------------------------- |
| **Decision**               | Can interrupt current process | Waits until current completes |
| **At Time 1**              | P1 (8) interrupted by P2 (4)  | P1 continues for 8 units      |
| **Total Completion Order** | P1 → P2 → P4 → P1 → P3        | P1 → P2 → P4 → P3             |
| **Avg Waiting Time**       | **6.5 units**                 | **9.25 units**                |

### Non-Preemptive Gantt Chart:

```
| P1 | P2 | P4 | P3 |
0    8    12   17   26
```

### WT in Non-Preemptive:

| Process | CT | TAT | WT |
| ------- | -- | --- | -- |
| P1      | 8  | 8   | 0  |
| P2      | 12 | 11  | 7  |
| P3      | 26 | 24  | 15 |
| P4      | 17 | 14  | 9  |

🧮 **Avg WT = (0 + 7 + 15 + 9)/4 = 31/4 = 7.75 units**

> So **preemptive SJF (SRTF)** is more efficient here.

---

## ✅ Summary

* **Preemptive SJF** dynamically chooses the shortest remaining job at every step, leading to lower waiting time.
* **Non-preemptive SJF** always waits for the current process to finish, even if a shorter job arrives later.


---
---
---




## ✅ **Preemptive SJF (SRTF)** – *Shortest Remaining Time First*

* It **checks continuously** (at every time unit) which process has the **shortest remaining burst time**.
* If a **new process arrives with a shorter burst time** than the currently running process, the CPU **immediately switches** (preempts) to that new process.
* So yes — if a process with **lower burst time arrives**, it will **interrupt** the current one.

---

### 🔁 Example from Your Case

| Process | Arrival | Burst |
| ------- | ------- | ----- |
| P1      | 0       | 7 - 1 = 6 |
| P2      | 1       | 4     |

At time = 0 → P1 starts
At time = 1 → P2 arrives (burst = 4 < 7 remaining of P1)
➡️ So CPU **switches from P1 to P2**!

---

## 🚫 Non-Preemptive SJF

* It **does NOT interrupt** the running process.
* Once a process starts, it **runs till completion**, even if a shorter job comes later.

---

### 🆚 Summary Table

| Feature              | Preemptive SJF (SRTF) | Non-Preemptive SJF |
| -------------------- | --------------------- | ------------------ |
| Interrupts running?  | ✅ Yes                 | ❌ No               |
| More efficient?      | ✅ Usually             | ❌ Sometimes worse  |
| Harder to implement? | ✅ Slightly            | ✅ Easier           |



---


# So we can say that this Preemptive-SJF will not gonna arrest of convoy effect