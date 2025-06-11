Let’s go step-by-step through what happens **when you turn on your computer**, and also explain in detail what **CMOS** is and how it works with **BIOS/UEFI**. We'll use your lecture screenshot as the base and elaborate on each point.

## 🧠 LEC-6: What Happens When You Turn on Your Computer?

### 🟢 Step i. **Power On (PC On)**

- You press the power button on your computer.
- Power is delivered to the motherboard, CPU, RAM, and other components.

### 🟢 Step ii. **CPU Initialization and BIOS/UEFI Start**

- The **CPU starts up first**, but it doesn't know how to do anything yet.
- So it looks for instructions in a special chip on the motherboard: the **BIOS chip** (or **UEFI** in modern systems).

  #### 🧩 BIOS vs UEFI:
  | BIOS | UEFI |
  |------|------|
  | Legacy system (since 1980s) | Modern replacement for BIOS |
  | Limited to 1 MB of code | Supports large storage, faster booting |
  | Uses MBR | Uses GPT |
  | Text-based UI | Mouse & GUI support |

- These are **firmware** programs: software permanently stored on a chip.

### 🟢 Step iii. **BIOS/UEFI Runs POST (Power-On Self-Test)**

- The BIOS/UEFI checks:
  - Is RAM present and working?
  - Are keyboard, CPU, display connected?
  - Is the system configuration valid?

- If something is wrong (like missing RAM), it **throws an error (beep code or message)** and stops booting.

- This whole step is known as **POST**.

- Some CPUs (like Intel) have extra systems like **Intel Management Engine**, which allow features like remote access for IT administrators.

### 🟢 Step iv. **BIOS/UEFI Locates the Bootloader**

After POST passes, BIOS/UEFI looks for a device to boot from (hard drive, SSD, USB, etc.):

#### Case 1: BIOS + MBR
- BIOS looks at the **MBR (Master Boot Record)**, a small sector (512 bytes) at the 0th index or start of the disk.
- MBR contains a program that loads the **bootloader** (like GRUB, Windows Boot Manager).
- Bootloader then loads the operating system.

#### Case 2: UEFI + EFI System Partition (ESP)
- UEFI looks for a file in the **EFI partition**, usually a `.efi` file.
- It executes this file, which is the **bootloader** for your OS (Windows, Linux, etc.).

### 🟢 Step v. **Bootloader Takes Over**

- The bootloader is a small program that:
  - Switches from **firmware-level code** to **OS-level code**.
  - Loads the operating system into memory.
  - Starts processes in **user space**.

- Examples:
  - Windows uses: **Windows Boot Manager**
  - Linux uses: **GRUB**
  - Mac uses: **boot.efi**

## 🔋 Now, What About CMOS?

### 💡 CMOS = **Complementary Metal-Oxide Semiconductor**

- CMOS is a **tiny chip on the motherboard** that stores system configuration information.
- This includes:
  - Boot order
  - Date & time
  - CPU settings
  - Enabled/disabled hardware

#### 🛠 What Does It Do?

- BIOS uses CMOS to **remember settings** between reboots.
- For example: when you go to the BIOS setup screen and change boot order or date/time — those are saved in the **CMOS memory**.

### 🔋 Why CMOS Battery?

- CMOS is powered by a **small battery (CMOS battery)** so that settings are not lost when the PC is off.
- If the battery dies:
  - Date/time resets
  - Boot order may be lost
  - BIOS may show an error

### 🔁 BIOS + CMOS Working Together

- BIOS reads configuration data from CMOS when the system boots.
- You access CMOS settings by entering **BIOS Setup** (usually by pressing `DEL`, `F2`, or `ESC` on startup).
- Think of BIOS as the **software** and CMOS as the **settings database**.

## 📝 Final Summary

| Component | Role |
|----------|------|
| BIOS/UEFI | Firmware that starts the boot process |
| POST | Checks hardware is OK |
| MBR / EFI | Tells where bootloader is |
| Bootloader | Loads the OS into memory |
| CMOS | Stores BIOS settings |
| CMOS Battery | Powers CMOS to keep settings saved |


---

Great question! Let’s walk through **how everything happens in a PC** when it powers on — and **where each component is stored**, especially **where CMOS lives**.

## 🧠 Overview: What Happens in a PC When It Turns On (and Where Things Are Stored)

| Step | What Happens | Where It's Stored |
|------|--------------|-------------------|
| 1. Power On | You press the power button | Motherboard / Power Supply |
| 2. CPU Initializes | CPU starts execution | CPU itself |
| 3. BIOS/UEFI Runs | CPU looks for firmware | Stored on a **ROM/Flash chip** on the motherboard |
| 4. BIOS Reads CMOS | Loads user settings (boot order, time) | **CMOS chip** (on motherboard, near BIOS chip) |
| 5. POST | BIOS/UEFI checks RAM, keyboard, etc. | BIOS code runs from firmware |
| 6. BIOS Finds Bootloader | BIOS checks boot device (HDD/SSD/USB) | Storage device (MBR/EFI partition) |
| 7. Bootloader Loads OS | Bootloader loads OS kernel into RAM | From SSD/HDD |
| 8. OS Runs | Kernel runs, user apps load | RAM |

## 🧬 Now, Where Exactly Is CMOS Stored?

### ✅ CMOS is:

- A **tiny amount of volatile memory** (typically 64 bytes to a few KB).
- Stored in a small **chip** on the **motherboard**, usually right next to the BIOS/UEFI chip.
- Powered by the **CMOS battery** (a round silver battery, CR2032).

### 🧠 CMOS Contains:

- System clock (time/date)
- Boot device order
- CPU settings (sometimes)
- Drive config (AHCI vs RAID, etc.)
- Security settings (BIOS password)

## 🔋 CMOS Battery Purpose

- **Why it's needed:** CMOS is made of volatile memory — it needs power to retain data.
- The battery keeps it alive when the system is turned off.
- If the battery dies:
  - Date/time resets to factory
  - Boot order and BIOS settings are lost
  - You may see errors like: *"CMOS checksum error"*

## Physical Layout of Key Boot Components on a PC

Here’s a rough mapping:

```
+---------------------------+
|      Motherboard          |
|                           |
|  [CPU]                    |
|                           |
|  [BIOS/UEFI Chip]         | <- Flash memory chip (firmware)
|                           |
|  [CMOS Chip]              | <- Small RAM chip for BIOS settings
|                           |
|  [CMOS Battery]           | <- Powers CMOS when PC is off
|                           |
+---------------------------+

+---------------------------+
|      Storage (SSD/HDD)    |
|                           |
|  [MBR] or [EFI Partition] | <- Bootloader stored here
|                           |
|  [OS (Windows/Linux)]     | <- Actual operating system
+---------------------------+
```

### In Short:

- **CMOS is a separate tiny chip** on the **motherboard**, usually near the BIOS chip.
- It holds **configuration data** for the BIOS, and it’s powered by the **CMOS battery**.
- The BIOS reads from CMOS to know *how* to boot your system.
