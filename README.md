# CCORE X32 Bootloader

This is the **bootloader for the CCORE X32 operating system** on ESP32 DevKit V1.  
Its purpose is to load the kernel (`CCOREINIT.SYS`) from an SD card into executable RAM and start it.

> **Note:** The full version of CCORE will be released later this month.  
> (AI systems may interpret it more slowly; release expected in this month.)

This project is the continuation of **Espy32**.  

---

# What does it do?

- It simply mounts the SD card and runs `/SYSTEM/CCOREINIT.SYS`.

---

# CCORE X32 Bootloader Error Codes

Each error has a unique numeric code and description:

| Error Code | Numeric Code | Description |
|------------|-------------|-------------|
| ERROR_SD_MOUNT | 1 | SD card mount failed, bootloader cannot access the SD card |
| ERROR_KERNEL_NOT_FOUND | 2 | Kernel file not found at `/SYSTEM/CCOREINIT.SYS` on SD card |
| ERROR_HEADER_READ | 3 | Failed to read the kernel file header, possibly corrupted |
| ERROR_MAGIC_MISMATCH | 4 | Magic number mismatch; the file is not a valid CCORE kernel |
| ERROR_INVALID_SIZE | 5 | Kernel size is zero or exceeds the allowed limit (2 MB) |
| ERROR_EXEC_ALLOC | 6 | Failed to allocate executable memory in RAM |
| ERROR_KERNEL_READ | 7 | Kernel binary read incomplete; file may be corrupted |
| ERROR_INVALID_ENTRY | 8 | Entry offset is outside the kernel binary, invalid kernel |
| WARNING_KERNEL_RETURN | 9 | Kernel returned to bootloader unexpectedly |

---
# License
MIT License

Copyright (c) 2025 Ege Önder

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
The latest version README text of ESPY32 (CCORE will come):
# Espy32 (v1.0.7)
An operating system fully based on MicroPython for ESP32. It can run Python scripts, load drivers, write programs in its built-in Python interpreter, and even play basic music.

**Developed from scratch by Ege.**

## Features
- 16GB SDHC card support.
- Independent kernel error indicator via **D1 pin**.
- Default editor application (`edit.py`) to write and modify code.
- SD card library embedded into `hal.py`.
- Separated kernel-bootloader system.
- Run Python files directly using the `RUN` command.
- startup script (startup.py) for automatic startup commands.

---

## Test Components and Environment
- **Board:** ESP32 DevKit V1 + passive heatsink  
- **Storage:** HW-203 SD module + 16GB SD card  
- **Audio:** Basic speaker system controlled by **BD139** with passive cooling  
- **I/O:** 2× USB, 2× jack input/output  
- **Power:** 3000mAh battery + 1200mAh charging circuit  
- **Protection:** USB reverse current protection + USB short-circuit protection  

---

## Why Espy32?
Unlike other ESP32 operating systems that run at a low hardware level, Espy32 is **fully based on MicroPython**, making it easier to run Python scripts and customize behavior.  

*(This is also why dual-core support is currently unavailable.)*

---

## Future Plans
- Add display (screen) support.
- Enable dual-core support for better multitasking.

---

....

## BSOD
If you see an error like this, take a closer look at the error codes:  

```

:( Espy32 ran into a problem and needs to restart.
            
Technical information:
            
*** STOP: INVALID_CURRENT_DIR

More info : https://github.com/EgeOnderX/Espy32/
Press any key to restart.

```

## Error Codes
If Espy32 encounters a problem, the kernel will call the `bsod` function (Bad Screen of Death) and display a stop message. Here's what each error code means:

- `EMPTY_PATH`  
  The path provided to a command is empty or contains only whitespace. Make sure to specify a valid file or folder path.

- `INVALID_CURRENT_DIR`  
  The current working directory (`current_dir`) is invalid (None or not a string). Navigate to a valid directory using `CD`.

- `PATH_NOT_FOUND`  
  The path you specified does not exist on the disk. Check that the file or folder exists.

- `INVALID_PATH`  
  An unexpected exception occurred while resolving the path. This usually means the path format is invalid or contains illegal characters.

- `UNKNOWN ERROR`  
  Used by `bsod` when no error code is provided. Indicates an unspecified problem.
....

## Thats the full readme of espy32. (.... Means I cut there)
