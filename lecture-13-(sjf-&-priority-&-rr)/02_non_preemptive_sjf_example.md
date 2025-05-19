Let's solve this using **SJF (Shortest Job First) – Non-preemptive** scheduling.

---

### 📋 Given Table

| Process | AT | BT |
| ------- | -- | -- |
| P1      | 0  | 8  |
| P2      | 1  | 4  |
| P3      | 2  | 9  |
| P4      | 3  | 5  |

---

### ✅ Step-by-step SJF Non-Preemptive Execution:

We’ll execute based on **shortest available burst time** at the time of CPU availability.

---

### 🕐 Time 0:

Only **P1** has arrived → Must start with P1

* **P1** runs from 0 to 8

---

### 🕐 Time 8:

By now, P2, P3, and P4 have all arrived because their arrival time is 1,2,3 seconds and we are already at the 8 seconds. Their BTs:

* P2 → 4
* P3 → 9
* P4 → 5

Choose **P2** (shortest BT, because non-preemptive sjf's rule is choose the shortest brust time)

* **P2** runs from 8 to 12

---

### 🕐 Time 12:

Remaining: P3 (BT = 9), P4 (BT = 5)
P4 has less BT so it will choose **P4**

* **P4** runs from 12 to 17

---

### 🕐 Time 17:

Only **P3** left

* **P3** runs from 17 to 26

---

### ✅ Completion Table

| Process | AT | BT | CT | TAT = CT - AT | WT = TAT - BT |
| ------- | -- | -- | -- | ------------- | ------------- |
| P1      | 0  | 8  | 8  | 8             | 0             |
| P2      | 1  | 4  | 12 | 11            | 7             |
| P4      | 3  | 5  | 17 | 14            | 9             |
| P3      | 2  | 9  | 26 | 24            | 15            |

---

### ✅ Gantt Chart

```
|  P1  |  P2  |  P4  |  P3  |
0      8      12     17     26
```

---

### ✅ Average Waiting Time

$$
\text{Avg WT} = \frac{0 + 7 + 9 + 15}{4} = \frac{31}{4} = \boxed{7.75}
$$




---

## If you are solving any question for SJF non-preemptive then remember that the question must have Arrival Time and Brust Time otherwise you will not gonna solve it

---

### ⚠️ Problem with SJF (Non-Preemptive)

1. **Starvation (Indefinite Blocking):**
   Long burst time processes may never get CPU if shorter ones keep arriving.
   Example: A process with BT = 20 could be postponed indefinitely.

2. **Requires Prior Knowledge:**
   SJF needs **exact burst time** of all processes in advance, which is not always possible.

3. **Not Realistic for Dynamic Systems:**
   In real-time OS, new processes keep arriving. SJF can't adapt well without constant re-evaluation.

4. **Poor for Interactive Systems:**
   SJF may cause poor response times for long processes even if they arrived early.

---

* **SJF Non-Preemptive only chooses from the processes that have arrived**.
* If **only P1 has arrived at 0**, no matter how long its burst time is, **it must be executed**.
* That means the system **can't "wait"** for P2 or P3 to arrive later and **compare** burst times **until** P1 finishes (since it’s **non-preemptive**).

### 🔍 Your Concern:

You’re saying:

* If **P1** arrives first and has a burst time of **80 seconds**, then **other processes must wait**, even if they have shorter burst times.
* You're implying that we **must always start with P1** just because it arrives first, and hence we can’t compare it with P2 or P3 that arrive later.

### 📘 Example:

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0            | 80         |
| P2      | 1            | 4          |
| P3      | 2            | 5          |


### ⛔ Convoy Effect:

* P1 comes at 0s → Start P1 immediately → Others wait for 80s → Convoy Effect

# To solve this type of convoy effect we need preemptive sjf