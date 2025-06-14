**Preemptive Priority Scheduling** Example

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

**Note:** higher priority number = **higher actual priority**

---

### ✅ Step-by-step Execution with Gantt Chart

#### 🔹 t = 0

* Only P1 has arrived
* So run **P1**
* ⏱️ Time: 0 → 1 (This will run for 1 sec because the preemptive priority scheduler will check is there any other higher priority process)

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |

#### 🔹 t = 1

* Arrived till now: P2
* So pick **P2**
* Run P2 from 1 → 2 (same it will also run for 1 sec and checks the next process)

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |


#### 🔹 t = 2

* Now arrived: P3
* Available = P1, P2
* So pick **P3**
* Run P3 → 2 to 3

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 3 - 1 = 2       |

#### 🔹 t = 3

* Now arrived: P4
* Remaining = P1, P2, P3
* So pick **P4**
* Run P4 → 3 to 5

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 3 - 1 = 2       |
| P4      | 10       | 3                 | 5 - 2 = 3       |

#### 🔹 t = 5

* Now arrived: P5 and P6
* Remaining = P1, P2, P3, P4
* Highest priority = **P6 (priority 12)**
* So pick **P6**
* Run P6 → 5 to 9

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 3 - 1 = 2       |
| P4      | 10       | 3                 | 5 - 2 = 3       |
| P5      | 8        | 4                 | 1               |
| P6      | 12       | 5                 | 4 - 4 = 0       |

 - means that **P6** process is completed

#### 🔹 t = 9

* Now arrived: P7
* Remaining = P1, P2, P3, P4, P5
* Highest priority = **P4 (priority 10)**
* So pick **P4**
* Run P4 → 9 to 12

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 3 - 1 = 2       |
| P4      | 10       | 3                 | 3 - 3 = 0       |
| P5      | 8        | 4                 | 1               |
| P7      | 9        | 6                 | 6               |

 - means that **P4** process is completed

#### 🔹 t = 12

* Remaining = P1, P2, P3, P5, P7
* Highest priority = **P7 (priority 4)**
* So pick **P7**
* Run P7 → 12 to 18

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 3 - 1 = 2       |
| P5      | 8        | 4                 | 1               |
| P7      | 9        | 6                 | 6 - 6 = 0       |

 - means that **P7** process is completed

#### 🔹 t = 18

* Remaining = P1, P2, P3, P5
* Highest priority = **P5 (priority 8)**
* So pick **P5**
* Run P5 → 18 to 19

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 3 - 1 = 2       |
| P5      | 8        | 4                 | 1 - 1 = 0       |

 - means that **P5** process is completed

#### 🔹 t = 19

* Remaining = P1, P2, P3
* Highest priority = **P3 (priority 6)**
* So pick **P3**
* Run P3 → 19 to 21

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 2 - 1 = 1       |
| P3      | 6        | 2                 | 2 - 2 = 0       |

 - means that **P3** process is completed

#### 🔹 t = 21

* Remaining = P1, P2
* Highest priority = **P2 (priority 4)**
* So pick **P2**
* Run P2 → 21 to 22

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 4 - 1 = 3       |
| P2      | 4        | 1                 | 1 - 1 = 0       |

 - means that **P2** process is completed

#### 🔹 t = 22

* Remaining = P1
* Priority = **P1 (priority 2)**
* Run P1 → 22 to 25

| Process | Priority | Arrival Time (AT) | Burst Time (BT) |
| ------- | -------- | ----------------- | --------------- |
| P1      | 2        | 0                 | 3 - 3 = 0       |

 - means that **P1** process is completed

 
Gantt chart:

### ✅ Gantt Chart

```
|  P1  |  P2  |  P3  |   P4   |   P6   |   P4   |   P7   |  P5  |  P3  |  P2  |   P1   |
0      1      2      3        5        9        12       18     19     21     22       25
```

---

### 📊 Completion Table



| Process | Priority | Arrival Time (AT) | Burst Time (BT) | CT | TAT (CT - AT) | WT (TAT - BT) |
| ------- | -------- | ----------------- | --------------- | -- | ------------- | ------------- |
| P1      | 2        | 0                 | 4               | 25 | 25            | 21            |
| P2      | 4        | 1                 | 2               | 22 | 21            | 19            |
| P3      | 6        | 2                 | 3               | 21 | 19            | 16            |
| P4      | 10       | 3                 | 5               | 12 | 9             | 4             |
| P5      | 8        | 4                 | 1               | 19 | 15            | 14            |
| P6      | 12       | 5                 | 4               | 9  | 4             | 0             |
| P7      | 9        | 6                 | 6               | 18 | 12            | 6             |

---

### 🧮 Average Waiting Time:


\| WT Sum = 21 + 19 + 16 + 4 + 14 + 0 + 6 = 80 |
\| Count = 7 processes |
\| Avg WT = 80 / 7 = **11.4** ✅ |

---

# This will also get arrested by Convoy Effect because if the highest priority process will continously coming then the lower priority will take a long long time
# Thats why we need Aging