# CustomLinuxOsShell
# MyOS

**MyOS** is a handcrafted, minimal Linux-like operating system, built from scratch with **C**, **assembly**, and a custom build system.  
This project is primarily educational — to learn how real operating systems like Linux boot, provide system calls, and launch user-space programs.  

The project culminates in a **custom minimal shell** (`/bin/sh`) that runs on MyOS.

---

## 📜 Features

- **Boot Process**
  - GRUB-based bootloader setup
  - Custom startup assembly (`start.S`, `crt0.S`)
  - ELF-based kernel and init process

- **System Calls**
  - Raw syscall interface implemented in assembly
  - Wrappers for essential syscalls (`write`, `read`, `open`, etc.)

- **Libraries**
  - `mylib/` as a **mini libc replacement** containing:
    - Syscall interface
    - Utility functions (`strlen`, delay, etc.)

- **Init Process**
  - First user-space program (`/sbin/init`)
  - Demonstrates printing to stdout, opening and reading files, and looping

- **Filesystem Layout**
  - Organized project structure with `init/`, `mylib/`, and `include/`
  - Installation into `/sbin` on a mounted disk image

- **Build System**
  - Modular `Makefile` system
  - Shared rules via `base.mk`
  - Supports clean builds and installation into mounted OS images

- **Custom Shell**
  - Minimal `/bin/sh` implementation
  - Reads user input and executes basic commands

---

## 📂 Project Structure

/project-root
│
├── base.mk # Shared Makefile rules (compilation, install, clean)
│
├── include/
│ └── mylib.h # Central header for syscall and utility declarations
│
├── init/
│ ├── Makefile
│ ├── crt0.S # Startup assembly for user programs
│ └── init.c # First user-space program (PID 1)
│
└── mylib/
├── Makefile
├── start.S # Entry point and syscall ABI setup
├── sys.c # Syscall wrappers
└── util.c # Utility functions (strlen, etc.)
|
└── lash/
├── Makefile
└── lash.c # Minimal custom shell source

---

## 🚀 How It Works

1. **Bootloader (GRUB)**  
   Loads the kernel (`vmlinuz`) and initial ramdisk (`initrd.img`).

2. **Kernel Initialization**  
   - Mounts the initrd as the root filesystem
   - Executes `/sbin/init`

3. **Init Program (`init.c`)**  
   - Prints a boot message
   - Demonstrates file I/O by opening and reading source files
   - Enters a simple event loop (printing `"TICK!"`)

4. **Shell (`/bin/sh`)**  
   - Accepts input from stdin
   - Executes basic commands
   - Represents the first interactive user program

---

## 🛠️ Building

Clone the repo:

```bash
git clone https://github.com/yourusername/myos.git
cd myos
```

Build Components:
```
make -C mylib
make -C init
```

Install Binaries into OS Image (/mnt/myos by default):
```
make -C init install
```

Clean Build artifacts:
```
make clean
```
