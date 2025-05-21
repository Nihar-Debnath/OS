### 🔒 What is the biggest problem of **locks**?

The biggest problems with locks are:

### ❌ 1. **Deadlock** (the most serious problem)

* This is **NOT busy waiting**, but much worse.
* Imagine two people trying to enter two different rooms, but each one has a key the other needs. Now both are **stuck forever**, waiting for each other.
* In programming, this is called **deadlock** — two (or more) threads wait forever, each holding a lock the other one needs.

So, **deadlock** is the **biggest and most dangerous** problem with locks.

---

### ❌ 2. **Busy Waiting** (not the biggest, but still a problem)

* Sometimes, a thread keeps checking, “Is the lock free? Is the lock free?” — again and again.
* This **wastes CPU** time — like someone knocking on a door nonstop instead of just waiting to be called.

**Condition Variables** help solve this problem by letting threads **sleep** instead of keep checking.

---

### ❌ 3. **Starvation**

* One thread **keeps getting skipped** and never gets the lock because other threads keep jumping in before it.

---
---

### 🧵 What is a Condition Variable?

Imagine you're standing in line to get inside a store, but the store only lets you in **when your number is called**. So, you're waiting, doing nothing, until someone calls your number.

This is what a **Condition Variable** does in programming:

* It allows a **thread** (like a person) to **wait** until some condition happens.
* The thread **doesn’t keep checking again and again** (which wastes time and energy).
* It just **sleeps peacefully** until it is **notified**.

---

### 🔒 It Works with a Lock

Before waiting, the thread must **lock the door** (use a lock) so no one else can change anything important.
But when it goes to sleep (waits), it **unlocks** so others can work.
When it's woken up, it **locks again** and continues working.

---

### 🧠 Why Use Condition Variables?

1. ✅ To **avoid busy waiting** — instead of checking every second, the thread just sleeps.
2. ✅ It helps **use system resources better** — no CPU is wasted.

---

### ❌ What is not here?

* **Contention** means many threads fighting over a resource. That’s not what this topic is about — so it's not discussed here.

### ❓ What does “Contention is not here” mean?

In the notes, under **Conditional Variable**, point **e** says:

> **e. Contention is not here.**

### 🤔 What is “Contention”?

**Contention** means **many threads trying to use the same resource at the same time** — like:

* Many people trying to enter the same bathroom.
* Many threads trying to use the same file or memory.

They are **competing** for it — so this is called **contention**.

### ✅ Now, what the notes are saying:

The focus of this lecture (about **Condition Variables**) is to explain **how threads wait for a condition without busy waiting**.

So, the author is saying:

> “We are not talking about contention (many threads fighting). That’s a different topic. Right now, we are only explaining how to wait properly using condition variables.”

### 🔁 In short:

> **“Contention is not here”** means
> 👉 “We are not discussing the case where threads are fighting for the resource.”
> 👉 “This topic is only about how to wait for a condition properly — not about resource competition.”

---

### 💡 Simple Analogy:

Imagine a kid waiting for ice cream.
He doesn’t keep asking, "Is it ready? Is it ready?" every second (that’s busy waiting).
Instead, he sits quietly, and **mom calls him** when the ice cream is ready.
That’s a **condition variable** in action.
