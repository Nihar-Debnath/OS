## ✅ **11. Advantages of Virtual Memory**

### a. **Increased Degree of Multi-Programming**

* **More programs can run at once**, even if the physical memory (RAM) is limited.
* Each program gets the **illusion of full memory** using virtual memory.
* OS **swaps pages in and out** as needed, so memory is shared efficiently.

> 🧠 Example: If you have 4 GB RAM but 8 GB worth of programs, virtual memory makes it possible to run them by keeping only the active parts in RAM.

---

### b. **Run Large Applications with Less Physical Memory**

* Programs **larger than the available RAM** can still run.
* Only **active (frequently used)** parts of a program are kept in memory.
* The rest stays in **swap space** (hard disk) until needed.

> 🧠 Example: Running Adobe Photoshop or a game on a system with low RAM still works because only the needed parts are loaded on-demand.

---

## ❌ **12. Disadvantages of Virtual Memory**

### a. **Slower System Performance (Swapping Time)**

* Accessing data from **swap (disk)** is **much slower than RAM**.
* If the system frequently swaps pages in and out, it can **slow down significantly**.

> ⚠️ Disk speed << RAM speed → Performance drops if paging happens often.

---

### b. **Thrashing**

* **Thrashing** happens when the system spends more time **swapping pages** than executing actual programs.
* Occurs when there are **too many active programs** or **too little RAM**.
* System becomes **almost unresponsive**.

> ⚠️ You click something and the system freezes or loads very slowly – this could be thrashing.

---

## 📌 Summary Table

| Advantages                         | Disadvantages            |
| ---------------------------------- | ------------------------ |
| Increases multi-programming        | Can slow down the system |
| Run large programs with little RAM | Thrashing may occur      |
