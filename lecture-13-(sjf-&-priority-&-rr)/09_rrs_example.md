Consider the following set of processes with their arrival times and burst times. Use **Round Robin scheduling** with a **Time Quantum (TQ) = 2 units**.

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P1      | 0                 | 4               |
| P2      | 1                 | 5               |
| P3      | 2                 | 2               |
| P4      | 3                 | 1               |
| P5      | 4                 | 6               |
| P6      | 6                 | 3               |

### ✅ **Solution:**

**Create a Gantt Chart using Round Robin (TQ = 2)**

We use a queue to keep track of processes. At each step, we execute a process for up to 2 units 
---or until it finishes.

#### 🔹 t = 0

* Only P1 has arrived
* **Queue**

```
|  P1  |
```
* So run **P1**
* ⏱️ Time: 0 → 2 (This will run for 2 sec because the time quantam is set to 2)

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |

---| P1      | 0                 | 4 - 2 = 2       |

#### 🔹 t = 2

* Arrived till now: P2, P3
* P1 being preempted (Brust time havent finished yet) and joins the queue again
* **Queue**
```
|  P2  |  P3  |   P1   |
```
* So pick **P2**
* Run P2 from 2 → 4 

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P1      | 0                 | 2               |
| P2      | 1                 | 5 - 2 = 3       |

---

#### 🔹 t = 4

* Now arrived: P4, P5
* P2 being preempted and joins the queue again
* **Queue**
```
|  P3  |   P1   |   P4   |   P5   |   P2   |
```
* So pick **P3**
* Run P3 → 4 to 6

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P1      | 0                 | 2               |
| P2      | 1                 | 3               |
| P3      | 2                 | 2 - 2 = 0       |
| P4      | 3                 | 1               |
| P5      | 4                 | 6               |
| P6      | 6                 | 3               |

 - means that **P3** process is completed at 6

---

#### 🔹 t = 6

* Now arrived: P6
* **Queue**

```
|   P1   |   P4   |   P5   |   P2   |   P6   |
```
* So pick **P1**
* Run P1 → 6 to 8

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P1      | 0                 | 2 - 2 = 0       |
| P2      | 1                 | 3               |
| P4      | 3                 | 1               |
| P5      | 4                 | 6               |
| P6      | 6                 | 3               |


--- - means that **P1** process is completed at 8

#### 🔹 t = 8

* **Queue**
```
|   P4   |   P5   |   P2   |   P6   |
```

* So pick **P4** (BT = 1)
* Because the P4 BT is 1 thats why it will only run 1 unit, it will not run the time quantum
* So run P4 → 8 to 9

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P2      | 1                 | 3               |
| P4      | 3                 | 1 - 1 = 0       |
| P5      | 4                 | 6               |
| P6      | 6                 | 3               |


--- - means that **P4** process is completed at 9

#### 🔹 t = 9

* **Queue**
```
|   P5   |   P2   |   P6   |
```
* So pick **P5**
* Run P5 → 9 to 11

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P2      | 1                 | 3               |
| P5      | 4                 | 6 - 2 = 4       |

---| P6      | 6                 | 3               |

#### 🔹 t = 11

* P5 being preempted (Brust time havent finished yet) and joins the queue again
* **Queue**
```
|   P2   |   P6   |    P5    |
```
* So pick **P2**
* Run P2 → 11 to 13

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P2      | 1                 | 3 - 2 = 1       |
| P5      | 4                 | 4               |
| P6      | 6                 | 3               |

---

#### 🔹 t = 13

* P2 being preempted (Brust time havent finished yet) and joins the queue again
* **Queue**
```
|   P6   |   P5   |   P2   |
```
* So pick **P6**
* Run P6 → 13 to 15

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P2      | 1                 | 1               |
| P5      | 4                 | 4               |
| P6      | 6                 | 3 - 2 = 1       |

---

#### 🔹 t = 15

* P6 being preempted (Brust time havent finished yet) and joins the queue again
* **Queue**
```
|   P5   |   P2   |   P6   |
```
* So pick **P5**
* Run P6 → 15 to 17

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P2      | 1                 | 1               |
| P5      | 4                 | 4 - 2 = 2       |
| P6      | 6                 | 1               |

---

#### 🔹 t = 17

* P5 being preempted (Brust time havent finished yet) and joins the queue again
* **Queue**
```
|   P2   |   P6   |   P5   |
```
* So pick **P2**
* Run P2 → 17 to 18

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P2      | 1                 | 1 - 1 = 0       |
| P5      | 4                 | 2               |
| P6      | 6                 | 1               |

 - means that **P2** process is completed at 18

---

#### 🔹 t = 18

* **Queue**
```
|   P6   |   P5   |
```
* So pick **P6**
* Run P6 → 18 to 19

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P5      | 4                 | 2               |
| P6      | 6                 | 1 - 1 = 0       |

 - means that **P6** process is completed at 19

---

#### 🔹 t = 19

* **Queue**
```
|   P5   |
```
* So pick **P5**
* Run P5 → 19 to 21

| Process | Arrival Time (AT) | Burst Time (BT) |
| ------- | ----------------- | --------------- |
| P5      | 4                 | 2 - 2 = 0       |

 - means that **P5** process is completed at 21


---

### ✅ Gantt Chart

```
|  P1  |  P2  |  P3  |   P1   |   P4   |   P5   |   P2   |  P6  |  P5  |  P2  |   P6   |   P5   |
0      2      4      6        8        9        11       13     15     17     18       19       21
```


---


### Time Quantum actually handle the overheading, means if time quantum increases then the process will run faster, and if the time quantum decreases then process will take a most of time to execute
## Just like this example we took TQ as 2 but is we have taken the TQ=4 then it will be much faster execution