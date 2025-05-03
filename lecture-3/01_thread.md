### 🔧 Imagine a Factory (Process) and Its Workers (Threads)

- A **process** is like a **factory**.
- Inside the factory, there are **workers** doing tasks — these are **threads**.

All the workers (threads):
- Share the same **building** (memory of the process),
- Use the same **tools and machines** (files, code, data),
- But each has their own **instructions** (stack, program counter).

### Example from Daily Life:

Suppose you open a web browser (like Chrome). That’s a **process**.

Now inside the browser:
- One tab is loading a YouTube video,
- Another tab is loading Google search,
- A third tab is running Gmail.

Each of these tasks is handled by a **separate thread**. All these threads belong to the same browser **process**, but they are doing different things **at the same time**.

### Why Use Threads?

- To **do many things at once** inside one program (process),
- To **save memory** because threads are lightweight,
- To **speed up performance** on multi-core CPUs.

### In Technical Terms:
A **thread** is like a mini-program running inside a bigger program.