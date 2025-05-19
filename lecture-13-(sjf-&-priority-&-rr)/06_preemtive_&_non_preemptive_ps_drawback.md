In **Priority Scheduling** (both **preemptive** and **non-preemptive**), the major **drawback** that can occur is:

---

## ⚠️ **Indefinite Blocking / Starvation**

### 🔍 What is it?

A **low-priority process** may **never get scheduled** if there are always **higher-priority processes** arriving in the system.

---

### 💡 Real-Life Analogy:

Imagine you're in a queue (like customer support). Every time your turn comes, someone with **“VIP”** status (higher priority) arrives and goes ahead of you. This keeps happening indefinitely — you might **never** get your turn.

---

## 🔴 In **Non-Preemptive Priority Scheduling**:

* Once a high-priority process gets CPU, it **runs till completion**.
* But **new lower-priority processes** keep getting **delayed** if higher-priority jobs keep arriving.
* A **low-priority job may wait forever** if higher-priority jobs never stop coming.

🛑 **Starvation can happen.**

---

## 🔴 In **Preemptive Priority Scheduling**:

* A low-priority process that starts executing can be **interrupted (preempted)** every time a higher-priority process arrives.
* So, it might **never complete** if there's a steady stream of higher-priority arrivals.

🛑 **Starvation still happens** (even more aggressively).

---

## ✅ Solution: **Aging**

To avoid starvation, we apply a technique called **aging**, where:

* The longer a process waits in the ready queue, the **higher its priority is gradually increased**.
* Eventually, even a low-priority process gets a chance to run.

---

### 📝 Summary Table:

| Aspect                            | Preemptive Priority | Non-Preemptive Priority |
| --------------------------------- | ------------------- | ----------------------- |
| Starvation (Indefinite wait)      | ✅ Yes               | ✅ Yes                   |
| Can a process be interrupted?     | ✅ Yes               | ❌ No                    |
| Needs Aging to prevent starvation | ✅ Yes               | ✅ Yes                   |