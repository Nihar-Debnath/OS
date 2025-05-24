## 🧠 **Topic: How Demand Paging Works**

---

## 🔟 What is Demand Paging?

**Demand Paging** is a virtual memory concept where:

* The OS does **not** load all pages of a process into RAM at once.
* Instead, it **loads pages only when they are actually needed**.
* This makes memory use efficient and saves time by avoiding loading unnecessary pages.

---

### ✅ (a) Page Prediction (Guessing)

> "When a process is to be swapped-in, the pager guesses which pages will be used."

* OS tries to **guess** what parts (pages) of the process will be used soon (this is just a prediction).
* This guess helps it avoid loading all pages blindly.

---

### ✅ (b) Partial Loading

> "The pager brings only those pages into memory which are likely to be used."

* This means: **Don’t load the entire program into RAM**.
* **Only load those pages that the process needs right now**.
* The rest are kept in the **disk (swap space)**.

---

### ✅ (c) Benefits

> "OS decreases the swap time and physical memory used."

* RAM is saved. ✅
* Time to load programs is reduced. ✅
* System becomes faster and more efficient. ✅

---

## 🧠 What is the Valid/Invalid Bit?

* Each page of a process has an entry in the **page table**.
* This entry includes a **valid/invalid bit** to track whether the page is in RAM or on the disk.

### ➤ Meaning:

| Bit Value     | Meaning                                                                                               |
| ------------- | ----------------------------------------------------------------------------------------------------- |
| `1` (Valid)   | The page is in memory and valid. ✅                                                                    |
| `0` (Invalid) | The page is either not valid (not part of the process) **or** it's valid but **on disk**, not in RAM. |

---

## 📘 **Title: Page Table When Some Pages Are Not in Memory**

### 📦 1. Logical Memory (Left Column)

This shows the **program's 8 pages** from 0 to 7, labeled as:

| Page No | Page Name |
| ------- | --------- |
| 0       | A         |
| 1       | B         |
| 2       | C         |
| 3       | D         |
| 4       | E         |
| 5       | F         |
| 6       | G         |
| 7       | H         |

These are the pages the process wants to use.

---

### 🧾 2. Page Table (Middle Column)

This table maps **each logical page** to:

* A **frame number** in physical memory.
* A **valid/invalid bit** (`1 = in RAM`, `0 = not in RAM`)

| Page No | Frame No | Valid Bit |
| ------- | -------- | --------- |
| 0 (A)   | 4        | 1 ✅       |
| 1 (B)   | —        | 0 ❌       |
| 2 (C)   | 6        | 1 ✅       |
| 3 (D)   | —        | 0 ❌       |
| 4 (E)   | —        | 0 ❌       |
| 5 (F)   | 9        | 1 ✅       |
| 6 (G)   | —        | 0 ❌       |
| 7 (H)   | —        | 0 ❌       |

> ❗NOTE: If the bit is 0, the page is not in memory → It's in the **swap space** (disk).

---

### 🧠 Summary from Page Table:

* Pages in **physical memory (valid = 1)**: A (0), C (2), F (5)
* Pages in **swap space (valid = 0)**: B (1), D (3), E (4), G (6), H (7)

---

### 🧠 3. Physical Memory (Right Side - Rectangles with Frame Numbers)

| Frame No | Page Stored |
| -------- | ----------- |
| 4        | A           |
| 6        | C           |
| 9        | F           |

These pages are **currently loaded in RAM**. Their corresponding page table entries have **valid bit = 1**.

---

### 💽 4. Swap Space (Disk - Cylindrical Shape)

This contains pages that are **NOT loaded into RAM**. Based on the page table:

Swap space has:

* Page B (1)
* Page D (3)
* Page E (4)
* Page G (6)
* Page H (7)

These pages will only be brought into memory if the process tries to use them. This triggers a **page fault**.

---

## 🔁 What Happens During Execution?

### ✅ If process accesses Page 0 (A):

* Valid bit = 1 → Frame = 4 → Found in RAM → No problem.

### ❌ If process accesses Page 3 (D):

* Valid bit = 0 → Not in memory → Page fault occurs.
* OS copies Page D from swap → Finds a free frame → Loads it → Updates page table.

---

## 🧠 Final Real-Life Analogy:

Think of **RAM as your desk**, and **swap space (disk)** as your bookshelf.

* You only keep **needed pages (A, C, F)** on your desk.
* The rest (B, D, E, G, H) are on the bookshelf.
* If you suddenly need Page D, you **get up**, bring it from the shelf (swap), and put it on your desk.
* If your desk is full, you might have to **remove something else** (page replacement).


---

## 🧠 What Happens During Access?

### ✅ (e) What if a page is never accessed?

> If a process never attempts to access some **invalid page**, it **runs fine**.

* No page fault.
* Process continues as if everything is okay.
* No need to load unneeded pages.

---

### 🚨 (f) What if a process accesses a missing (invalid) page?

> If the page is not in memory and is needed...

* The **CPU checks the page table**, sees the **valid bit = 0**.
* It causes a **page fault**.
* Page fault = OS is **interrupted** to bring the page from **disk (swap)** to **RAM**.
* OS chooses a **free frame** (or uses page replacement), **loads the page**, and updates the page table.

---

## 🧠 Summary

| Concept           | Meaning                                          |
| ----------------- | ------------------------------------------------ |
| Virtual Memory    | Illusion of large memory by using disk           |
| Demand Paging     | Only load pages into memory when needed          |
| Page Fault        | Happens when a required page is not in memory    |
| Valid/Invalid Bit | Tells if the page is currently in RAM or not     |
| Swap Space        | Disk area to store pages not in RAM              |
| Pager             | Component that handles individual page transfers |
