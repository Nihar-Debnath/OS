**Non-Preemptive Priority Scheduling**, meaning **once a process starts executing, it runs to completion**, and the **next process is chosen based on the highest priority** among the **arrived processes only**.

---

### 📋 Given Data

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4               |
| P2      | 4        | 1                 | 2               |
| P3      | 6        | 2                 | 3               |
| P4      | 10       | 3                 | 5               |
| P5      | 8        | 4                 | 1               |
| P6      | 12       | 5                 | 4               |
| P7      | 9        | 6                 | 6               |


---

### 🧠 Non-Preemptive Priority Scheduling Logic

We simulate time from **t = 0** onward. At every time a process finishes, we:

* Check all **arrived processes**
* Select the one with **highest priority (lowest number)**
* Run it to **completion** (non-preemptive)

---

### ✅ Step-by-step Execution with Gantt Chart

#### 🔹 t = 0

* Only P1 has arrived
* So run **P1** (BT=4)
* ⏱️ Time: 0 → 4

#### 🔹 t = 4

* Arrived till now: P2, P3, P4, P5
* Highest priority = **P4 (priority 10)**
* So pick **P4** (BT=5)
* Run P4 from 4 → 9

#### 🔹 t = 9

* Now arrived: P6, P7
* Available = P3, P4, P5, P6, P7
* Highest priority among them = **P6 (priority 12)**
* So pick **P6** (BT=4)
* Run P6 → 9 to 13

#### 🔹 t = 13

* Remaining = P2 (4), P3 (6), P5 (8), P7 (9)
* Highest priority = **P7 (priority 9)**
* So pick **P9** (BT=6)
* Run P9 → 13 to 19

#### 🔹 t = 19

* Remaining = P2 (4), P3 (6), P5 (8)
* Highest priority = **P5 (priority 8)**
* So pick **P5** (BT=1)
* Run P5 → 19 to 20

#### 🔹 t = 20

* Remaining = P2 (4), P3 (6)
* Highest priority = **P3 (priority 6)**
* So pick **P3** (BT=3)
* Run P3 → 20 to 23

#### 🔹 t = 23

* Remaining = P2 (4)
* Highest priority = **P2 (priority 4)**
* So pick **P2** (BT=2)
* Run P2 → 23 to 25


Gantt chart:

### ✅ Gantt Chart

```
|  P1  |  P4  |  P6  | P7 |     P5     |     P3     |  P2  |
0      4      9      13   19           20           23     25
```


---

### 📊 Completion Table



| Process | Priority | Arrival Time (AT) | Burst Time (BT) | CT | TAT (CT - AT) | WT (TAT - BT) |
| ------- | -------- | ----------------- | --------------- | -- | ------------- | ------------- |
| P1      | 2        | 0                 | 4               | 4  | 4             | 0             |
| P2      | 4        | 1                 | 2               | 25 | 24            | 22            |
| P3      | 6        | 2                 | 3               | 23 | 22            | 19            |
| P4      | 10       | 3                 | 5               | 9  | 6             | 1             |
| P5      | 8        | 4                 | 1               | 20 | 16            | 15            |
| P6      | 12       | 5                 | 4               | 13 | 8             | 4             |
| P7      | 9        | 6                 | 6               | 19 | 14            | 7             |

---

### 🧮 Average Waiting Time:


\| WT Sum = 0 + 22 + 19 + 1 + 15 + 4 + 7 = 68 |
\| Count = 7 processes |
\| Avg WT = 68 / 7 = **9.71** ✅ |

---

# This will also get arrested by Convoy Effect if the first process will come in more Brust time