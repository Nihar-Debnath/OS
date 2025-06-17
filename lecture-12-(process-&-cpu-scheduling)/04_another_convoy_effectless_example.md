# So here we just rotated the process from previous example

### 📋 Given Data:

| Pno | AT | BT |
| --- | -- | -- |
| P2  | 0  | 2  |
| P3  | 1  | 2  |
| P1  | 2  | 20 |

---

### ✅ Step 1: Sort by Arrival Time (AT)

Already sorted:

**Execution Order:** P2 → P3 → P1

---

### ✅ Step 2: Calculate Completion Time (CT)

Start time is 0.

* **P2**: Starts at 0 → CT = 0 + 2 = **2**
* **P3**: Starts at 2 → CT = 2 + 2 = **4**
* **P1**: Starts at 4 → CT = 4 + 20 = **24**

---

### ✅ Step 3: Turnaround Time (TAT = CT - AT)

| Pno | AT | CT | TAT |
| --- | -- | -- | --- |
| P2  | 0  | 2  | 2   |
| P3  | 1  | 4  | 3   |
| P1  | 2  | 24 | 22  |

---

### ✅ Step 4: Waiting Time (WT = TAT - BT)

| Pno | TAT | BT | WT |
| --- | --- | -- | -- |
| P2  | 2   | 2  | 0  |
| P3  | 3   | 2  | 1  |
| P1  | 22  | 20 | 2  |

---

### ✅ Final Table

| Pno | AT | BT | CT | TAT | WT |
| --- | -- | -- | -- | --- | -- |
| P2  | 0  | 2  | 2  | 2   | 0  |
| P3  | 1  | 2  | 4  | 3   | 1  |
| P1  | 2  | 20 | 24 | 22  | 2  |

---

### ✅ Gantt Chart

```
| P2 | P3 |      P1       |
0    2    4              24
```

---

### ✅ Average Waiting Time

$$
\text{Avg WT} = \frac{0 + 1 + 2}{3} = \frac{3}{3} = 1
$$

see here the avg wt is 1, so that means a big process will come at first then that process will cause a convoy effect