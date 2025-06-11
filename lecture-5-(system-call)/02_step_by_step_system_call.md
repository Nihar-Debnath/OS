## 🧪 Your Script: `hello.sh`

```sh
#!/bin/bash
while [ true ]
do
    echo "hello nihar!"
    sleep 1
done
```

This script:
1. Continuously prints "hello nihar!" every second.
2. Runs inside a shell (Bash), which interacts with the kernel using **system calls**.

Now let’s analyze system calls **step by step**.

## ✅ Step 1: Creating the file `hello.sh`

When you create a file (`hello.sh`) using a text editor or `touch` or `echo >`, you are using system calls like:

- `open()` – Open or create the file.
- `write()` – Write the script content to the file.
- `close()` – Close the file after writing.

## ✅ Step 2: Running the script

```sh
bash hello.sh
```

Here, Bash:
1. Executes a new script file.
2. Reads the contents of `hello.sh`.
3. Executes commands line-by-line.

### System calls used here:
- `fork()` – Bash forks a new process to run the script.
- `execve()` – The new process replaces its image with `bash` executing `hello.sh`.
- `open()` – The file is opened for reading.
- `read()` – Bash reads the file line by line.
- `fstat()` – Check file metadata (e.g., permissions).
- `mmap()` – May be used to load parts of the file into memory.

## ✅ Step 3: Inside the `while` loop

This part runs forever:
```sh
echo "hello nihar!"
sleep 1
```

### `echo` command:

`echo` internally uses:

- `write()` – to print to `stdout` (usually your terminal).
- Possibly `open()` and `close()` if writing to a file or pipe.

### `sleep 1` command:

This pauses for 1 second using:

- `nanosleep()` or `clock_nanosleep()` system call – tells the OS to pause the process.

And every loop iteration also likely involves:

- `read()` – to interpret the next line.
- `dup()` – duplicate file descriptors (stdout, etc.)

## ✅ Step 4: Checking processes

```sh
ps -a
```

This command:

- Opens and reads from `/proc` filesystem (a virtual filesystem that holds process information).
- Uses system calls:
  - `open()`, `read()`, `getdents()` – to read process info.
  - `stat()` – to check file info.
  - `mmap()` – possibly to load process info efficiently.

## ✅ Step 5: Killing the process

```sh
kill <pid>
```

This command uses:

- `kill()` system call – sends a signal (like `SIGTERM`) to the process.
  - The signal is handled by the kernel.
  - The target process receives it and may terminate.

## 📊 Summary: System Calls Involved

| Action                 | System Calls Used                                             |
|------------------------|--------------------------------------------------------------|
| Creating the file      | `open()`, `write()`, `close()`                               |
| Running the script     | `fork()`, `execve()`, `open()`, `read()`, `mmap()`, `fstat()`|
| `echo` inside script   | `write()`                                                    |
| `sleep` inside script  | `nanosleep()`                                                |
| Checking with `ps`     | `open()`, `read()`, `getdents()`, `stat()`, `mmap()`         |
| Killing the process    | `kill()`                                                     |

➤ **At least 10+ distinct system calls** are used in total, many of them are called repeatedly inside the loop.
