## 🧠 **What is a Page Fault?**

A **page fault** occurs when a program tries to access a **page that is not currently in physical memory (RAM)**. That page is instead in the **swap space (disk)**.

---

## 🔍 **Diagram Breakdown: Steps in Handling a Page Fault**

### ⚙️ 1. Reference Made (🔁 Step 1)

* The process tries to **load memory location M** (e.g. `load M`).
* Memory address `M` is **translated using the page table**.
* The **page table** shows that the page is **not in memory** (valid bit = 0).

---

### ⚠️ 2. Trap to the OS (Step 2)

* A **trap** (software interrupt) is generated.
* The **Operating System (OS)** takes control to handle the fault.

---

### 🔎 3. OS Checks Page Validity (Step 3)

* OS checks the **PCB (Process Control Block)**:

  * **Is this a valid memory reference?**
  * If **invalid**: Process is terminated with a **segmentation fault**.
  * If **valid**: The page exists but is in **swap (backing store)**.

---

### 🧱 4. Find Free Frame + Bring in Page (Step 4)

* OS **searches for a free frame** in physical memory.
* It **schedules a disk I/O operation** to read the page from **swap space into RAM**.

---

### ✅ 5. Update Page Table (Step 5)

* When the disk I/O is done:

  * The **page is now in memory**.
  * The **page table is updated** with the **new frame number**.
  * The **valid bit is set to 1**.

---

### 🔁 6. Restart the Instruction (Step 6)

* The instruction that caused the page fault is **restarted**.
* Now the page is available in memory, so execution **continues smoothly**.

---

## 🔄 Summary Table

| Step | Description                                               |
| ---- | --------------------------------------------------------- |
| 1    | Process references address `M` (page not in memory).      |
| 2    | OS is notified (trap) due to page fault.                  |
| 3    | OS checks if memory reference is valid.                   |
| 4    | If valid, OS finds a free frame and reads page from swap. |
| 5    | OS updates the page table.                                |
| 6    | The original instruction is restarted.                    |

---

## 🔥 Additional Theoretical Points

### ✅ g. Stepwise Procedure to Handle Page Fault

| Step | Explanation                                                                            |
| ---- | -------------------------------------------------------------------------------------- |
| i    | OS checks if memory reference is valid using the PCB.                                  |
| ii   | If **invalid**: throw **exception** (segmentation fault). If **valid**: start swap-in. |
| iii  | Find a free frame (from free-frame list).                                              |
| iv   | Disk operation brings the page into that free frame.                                   |
| v    | Update page table → now page is in memory.                                             |
| vi   | Restart the instruction → now works as if page was always present.                     |

---

### 💡 h. Pure Demand Paging

* In **pure demand paging**, **no pages are loaded initially**.
* Execution starts, **every access causes a page fault**.
* Pages are loaded **only when accessed** (lazy loading).

Example:

* Process starts, tries to execute first instruction → Page fault → OS brings that page.
* Keeps repeating until enough pages are in memory for smooth execution.

---

### 📍 i. Locality of Reference

Demand paging performs well **because of the principle of locality**:

* **Temporal locality**: Recently accessed pages are likely to be used again.
* **Spatial locality**: Pages near the current page are likely to be used soon.

So, even if we bring pages on-demand, they’re likely to be useful repeatedly.

---

## 📌 TL;DR – Key Concepts

| Concept       | Meaning                                |
| ------------- | -------------------------------------- |
| Page fault    | When needed page is not in RAM         |
| Trap          | OS interrupt to handle fault           |
| Swap          | Disk area holding non-RAM pages        |
| Page Table    | Tells whether page is in memory or not |
| Valid Bit     | 1 = in RAM, 0 = in swap                |
| Demand Paging | Load page only when accessed           |
| Locality      | Helps reduce number of faults          |