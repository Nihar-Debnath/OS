### 🧠 **Concept of FCFS Scheduling**

**FCFS (First Come First Serve)** is the simplest scheduling algorithm.

* The **process which arrives first gets executed first**.
* If two processes have the same arrival time, the one with the lower process number is prioritized.
* It’s **non-preemptive** (once a process starts, it runs till completion).
* So it can cause **Convoy Effect**.

---

### 📋 Given Data (from your image):

| Pno | AT (Arrival Time) | BT (Burst Time) |
| --- | ----------------- | --------------- |
| P1  | 0                 | 20              |
| P2  | 1                 | 2               |
| P3  | 2                 | 2               |

---

### ✅ Step-by-Step Rules to Solve FCFS Questions

---

#### 🔹 **Step 1: Sort the processes by Arrival Time (AT)**

If same AT, use process number as tie-breaker.

Here:

* P1 (AT=0)
* P2 (AT=1)
* P3 (AT=2)

So the order remains: **P1 → P2 → P3**

---

#### 🔹 **Step 2: Calculate Completion Time (CT)**

* `CT` is when the process **finishes executing**.
* Use a running timeline starting from 0.

```text
Time = 0
P1 starts at 0 and runs for 20 → CT of P1 = 0 + 20 = 20
P2 starts at 20 and runs for 2 → CT of P2 = 20 + 2 = 22
P3 starts at 22 and runs for 2 → CT of P3 = 22 + 2 = 24
```

| Pno | AT | BT | CT |
| --- | -- | -- | -- |
| P1  | 0  | 20 | 20 |
| P2  | 1  | 2  | 22 |
| P3  | 2  | 2  | 24 |

---

#### 🔹 **Step 3: Calculate Turnaround Time (TAT)**

$$
TAT = CT - AT
$$

| Pno | CT | AT | TAT |
| --- | -- | -- | --- |
| P1  | 20 | 0  | 20  |
| P2  | 22 | 1  | 21  |
| P3  | 24 | 2  | 22  |

---

#### 🔹 **Step 4: Calculate Waiting Time (WT)**

$$
WT = TAT - BT
$$

| Pno | TAT | BT | WT |
| --- | --- | -- | -- |
| P1  | 20  | 20 | 0  |
| P2  | 21  | 2  | 19 |
| P3  | 22  | 2  | 20 |

---

#### 🔹 **Step 5: Draw the Gantt Chart**

```
|  P1  |  P2  |  P3  |
0     20     22     24
```

---

#### 🔹 **Step 6: Calculate Average Waiting Time (Avg WT)**

$$
\text{Avg WT} = \frac{0 + 19 + 20}{3} = \frac{39}{3} = 13
$$

Here the Avg WT is 13 seconds because of the convoy effect but if we rotate all the process then we will see a change
Read the **04_another_convoy_effectless_example.md** for understanding hpw the convoy effects happens


---

### ✅ Final Answer Summary:

| Pno | AT | BT | CT | TAT | WT |
| --- | -- | -- | -- | --- | -- |
| P1  | 0  | 20 | 20 | 20  | 0  |
| P2  | 1  | 2  | 22 | 21  | 19 |
| P3  | 2  | 2  | 24 | 22  | 20 |

* **Average WT = 13**
* **Gantt Chart:** `| P1 | P2 | P3 |` → `0 20 22 24`

---

### 🧾 Key Formulas Recap:

* **Completion Time (CT)**: When a process completes = Start Time + Burst Time
* **Turnaround Time (TAT)**: `TAT = CT - AT`
* **Waiting Time (WT)**: `WT = TAT - BT`
* **Average Waiting Time**: `Avg WT = Sum(WT) / Number of Processes`
