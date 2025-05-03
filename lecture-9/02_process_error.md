Both the **stack** and **heap** are essential memory regions in a running process—but if they're misused, they can lead to serious errors or even crash your program. Let’s look at the **common errors**, **why they happen**, and **how to fix them**.

## 🗂️ STACK ERRORS

### 🔴 1. **Stack Overflow**
**What happens:** You use **too much stack memory**, usually by:
- **Too many nested function calls**
- **Infinite recursion**
- Declaring **large local variables** (e.g., `int arr[1000000];` inside a function)

**Symptoms:**
- Program crashes
- Segmentation fault
- “Stack overflow” message (in some languages)

**Fixes:**
✅ Avoid deep or infinite recursion  
✅ Use heap allocation (`malloc`/`new`) for large arrays instead of local variables  
✅ Break problems into **iterative** solutions when possible

### 🟡 2. **Uninitialized Variables**
**What happens:** You use a local variable (on the stack) without initializing it.

**Symptoms:**
- Garbage values
- Unpredictable behavior
- Security issues (may expose leftover data)

**Fixes:**
✅ Always initialize local variables before using them  
✅ Use compiler warnings (like `-Wall` in GCC) to catch them

## 🗃️ HEAP ERRORS

### 🔴 1. **Memory Leak**
**What happens:** You allocate memory on the heap but **never free it**.

**Symptoms:**
- Program uses more and more memory over time
- Slows down or crashes
- Detected with memory profiling tools

**Fixes:**
✅ Always `free()` (C) or `delete` (C++) what you `malloc()` or `new`  
✅ Use smart pointers in C++ (`unique_ptr`, `shared_ptr`)  
✅ Use memory tools:  
- **Valgrind** (Linux)  
- **Visual Leak Detector** (Windows)

### 🔴 2. **Dangling Pointer**
**What happens:** You free memory, but still try to use it.

```c
int* ptr = malloc(4);
free(ptr);
*ptr = 10; // ❌ Using freed memory
```

**Symptoms:**
- Crash
- Corrupt data
- Security vulnerabilities

**Fixes:**
✅ After `free(ptr)`, always do `ptr = NULL;`  
✅ Avoid manually managing memory if possible—use safe abstractions

### 🔴 3. **Double Free**
**What happens:** You call `free()` on the same pointer **twice**.

**Symptoms:**
- Crash
- Heap corruption
- Undefined behavior

**Fixes:**
✅ Set pointer to `NULL` after freeing  
✅ Track ownership carefully  
✅ Use tools like **ASAN** (AddressSanitizer) to detect this

### 🔴 4. **Buffer Overflow / Underrun**
**What happens:** You write more data into a heap/stack buffer than it can hold.

```c
char buf[10];
strcpy(buf, "This is way too long!"); // ❌ Overflows buffer
```

**Symptoms:**
- Data corruption
- Crashes
- Exploitable security flaws

**Fixes:**
✅ Use safer functions (`strncpy`, `snprintf`)  
✅ Avoid raw pointer arithmetic  
✅ Use languages or tools with bounds checking (like Rust or sanitizers in C)

## ✅ Summary Table

| Error | Where | Cause | Fix |
|-------|-------|-------|-----|
| Stack Overflow | Stack | Deep recursion or large local variables | Use loops, allocate large data on heap |
| Uninitialized Variable | Stack | Using before assigning | Always initialize |
| Memory Leak | Heap | No `free()` after `malloc()` | Free memory properly, use tools |
| Dangling Pointer | Heap | Using memory after free | Set pointer to `NULL` after free |
| Double Free | Heap | Calling `free()` twice | Track pointer ownership |
| Buffer Overflow | Both | Writing beyond buffer size | Use safe APIs, validate size |
