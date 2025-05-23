# 🧾 2. **How Free Space is Stored in OS?**

---

> Free memory blocks (or **holes**) are stored in a **Free List**.

---

### 💻 **Free List = Linked List** 📋

Each hole is a **node** in the linked list.

Each node stores:

* Starting address of free block
* Size of the block
* Pointer to the next free hole

Why Linked List?

* It’s dynamic in size
* Easy to insert/delete nodes (holes)
* Efficient for managing varying hole sizes

---

## 👨‍🏫 Friendly Example:

Imagine a notebook with bookmarks for blank pages.

* Each bookmark tells you:

  * Where the blank page starts
  * How big it is
  * Where the next blank page is

This is exactly what the **Free List** does.

---

# 📌 3. **How OS Allocates Memory from Free List?**

When a process needs memory of size `n`, the OS **searches the free list** using one of several algorithms.

---

### Let's Explore Each Allocation Strategy:

---

## 🔹 a. **First Fit**

---

### 💻 Computer Logic:

* Start from the **beginning of the free list**.
* Allocate the **first hole** that is **big enough** for the process.
* If the hole is **larger than needed**, **split it** — keep the extra part in the free list.

---

### 👨‍🏫 Friendly View:

You enter a theater and need 4 seats.

* You find the **first row** with at least 4 empty seats.
* You take those and move on.

Simple, fast, no drama.

---

### ✅ Pros:

* Fast (shorter search time)
* Easy to implement

### ❌ Cons:

* May leave many small unused holes **near the beginning** of memory

---

## 🔹 b. **Next Fit**

---

### 💻 Computer Logic:

* Like First Fit, **but** the search **starts from where the last allocation ended**.
* Circular search through the free list.

---

### 👨‍🏫 Friendly View:

You're at a buffet.

* You filled your plate at one counter.
* Next time, instead of starting from the entrance, you **continue from the last counter you visited**.

---

### ✅ Pros:

* Avoids clustering at the beginning
* Spreads allocations across memory

### ❌ Cons:

* May be slower than First Fit in some cases
* Can still cause fragmentation

---

## 🔹 c. **Best Fit**

---

### 💻 Computer Logic:

* Search the **entire free list**.
* Find the **smallest hole** that is still **big enough**.
* Allocate from that hole to **minimize leftover space**.

---

### 👨‍🏫 Friendly View:

You're packing books into boxes.

* You want to find the **smallest box** that **just fits** the book.
* No big box for a small book.

---

### ✅ Pros:

* Less **internal fragmentation**
* Efficient use of memory per allocation

### ❌ Cons:

* Slower (must search whole list)
* Leaves behind **many tiny unusable holes** (external fragmentation)

---

## 🔹 d. **Worst Fit**

---

### 💻 Computer Logic:

* Search the **entire list**.
* Pick the **largest available hole**.
* Allocate from that.

---

### 👨‍🏫 Friendly View:

You have a huge suitcase.

* Instead of finding a tight-fitting bag for your shoes, you just throw them into the **biggest** bag you can find.

The rest of the bag can be reused for other stuff.

---

### ✅ Pros:

* Leaves **larger leftover holes** — which may be useful for future big processes

### ❌ Cons:

* Very inefficient
* Slower search
* May still lead to fragmentation

---

## ⚔️ Comparison Table:

| Strategy  | Speed   | Fragmentation Risk     | Search Area          | Good For                    |
| --------- | ------- | ---------------------- | -------------------- | --------------------------- |
| First Fit | Fastest | Moderate               | From beginning       | Simple, general purpose     |
| Next Fit  | Fast    | Moderate               | From last allocation | Spreading allocations       |
| Best Fit  | Slow    | External (small holes) | Entire list          | Minimizing unused space     |
| Worst Fit | Slowest | Internal               | Entire list          | Preparing for big processes |

---

# ✅ Final Thoughts:

* **Compaction** helps clean up fragmentation but is costly in CPU terms.
* **Free space is tracked** using a Linked List.
* **Memory allocation strategies** (First Fit, Best Fit, etc.) are like **decision-making brains** of the OS to decide where to place processes.

---
---
---
---

### 🔍 Given Free Holes in RAM (Random scattered holes):

```
[  0 –  5 ]  = Used (OS)
[  5 – 10 ] = Free (5 KB)
[ 10 – 15 ] = Used (P1)
[ 15 – 30 ] = Free (15 KB)
[ 30 – 40 ] = Used (P2)
[ 40 – 60 ] = Free (20 KB)
```

Now a new process **P3 = 12 KB** needs to be placed. Let's apply all 4 algorithms:

---

## 🟡 **1. First Fit**

🔎 **Find the first hole that's big enough**.

```
Step 1: [5 – 10] → 5 KB → ❌ Not enough
Step 2: [15 – 30] → 15 KB → ✅ Fit here!
```

✅ So P3 goes in `[15 – 27]`, and 3 KB remains as new free hole.

```
Result (First Fit):
[15 – 27] = P3
[27 – 30] = Free (3 KB)
```

**✅ Fast** and simple — just takes the **first match**.

---

## 🔵 **2. Next Fit**

🔁 **Like First Fit**, but instead of starting from top, it starts **where it last left off**.

Let’s say **last process (P2)** was placed at `[30 – 40]`. So we start search **from after 40**:

```
Step 1: [40 – 60] → 20 KB → ✅ Big enough
```

✅ So P3 goes in `[40 – 52]`, 8 KB remains free.

```
Result (Next Fit):
[40 – 52] = P3
[52 – 60] = Free (8 KB)
```

**✅ Same logic as First Fit**, but optimizes repeated searches.

---

## 🟢 **3. Best Fit**

🎯 **Find the smallest hole that still fits**.

From all free holes:

- [5 – 10] = 5 KB ❌ too small
- [15 – 30] = 15 KB ✅ candidate
- [40 – 60] = 20 KB ✅ candidate

Now pick the **smallest among those** that fits 12 KB → `15 KB is smallest`.

✅ So P3 placed in `[15 – 27]` again, 3 KB left.

```
Result (Best Fit):
[15 – 27] = P3
[27 – 30] = Free (3 KB)
```

**✅ Less internal waste**, but may **cause many small scattered holes** = *external fragmentation*.

---

## 🔴 **4. Worst Fit**

💥 **Opposite of Best Fit**. Use the **biggest hole available**.

From free holes:

- [5 – 10] = 5 KB ❌ too small
- [15 – 30] = 15 KB ✅
- [40 – 60] = 20 KB ✅ → biggest

So we put P3 in `[40 – 52]`, leaving 8 KB.

```
Result (Worst Fit):
[40 – 52] = P3
[52 – 60] = Free (8 KB)
```

✅ Leaves big holes behind that might be useful later.  
❌ But **search is slow**, and logic is not always efficient.

---

## 🧠 Summary Table

| Algo       | How it Chooses              | Pros                          | Cons                         |
|------------|-----------------------------|-------------------------------|------------------------------|
| **First Fit** | First block that fits         | Fast, simple                  | May leave gaps early in list |
| **Next Fit**  | From last placed block        | Saves time for next calls     | Might skip good earlier holes |
| **Best Fit**  | Smallest suitable block       | Less internal fragmentation   | Creates many small holes     |
| **Worst Fit** | Largest suitable block        | Leaves room for future        | High external fragmentation  |