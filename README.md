# Kernel Modules

## Description
This repository contains the practical development and research corresponding to TP N°4 for the Sistemas de Computación course (FCEFyN - UNC, 2026). The project focuses on the design, compilation workflow, execution analysis, and lifecycle of Loadable Kernel Modules (LKM) within Linux environments.

Through this work, we examine execution environments with differentiated hardware privileges (User Space vs. Kernel Space), monitor system calls using the `strace` diagnostic tool, and document the cryptographic security mechanisms (Secure Boot, `mokutil`, and `sign-file`) used to prevent the unauthorized execution of code at Ring 0 (rootkits).

---

## Requirements & Installation

To configure the development environment and compile external (out-of-tree) kernel modules, you must install the essential build utilities and the kernel headers corresponding to your Linux distribution:

### On Debian/Ubuntu-based systems:
 ```bash
 sudo apt-get update
 sudo apt-get install build-essential checkinstall kernel-package linux-source
 ```
### On Arch Linux / EndeavourOS-based systems:
 ```bash
 sudo pacman -Syu base-devel linux-lts-headers
 ```
---

## Usage Instructions

### 1. Compiling and Managing the Experimental Module
The source code for the controller is located inside the `part1` directory. To compile, load, and unload the module from the system, execute the following sequence of commands:

#### Navigate to the module directory
```bash
$ cd part1
```
#### Compile the source code using the Makefile
```bash
$ make
```
#### Dynamically insert the module into kernel space
```bash
$ sudo insmod mimodulo.ko
```
#### Verify that the module is active in RAM
```bash
$ lsmod | grep mod
$ cat /proc/modules | grep mod
```
#### Remove or unload the module from the kernel
```bash
$ sudo rmmod mimodulo
```
### 2. Monitoring Kernel Logs
To audit the initialization (init_module) and exit (cleanup_module) messages printed by the controller to the kernel ring buffer, use:
```bash
$ sudo dmesg
```
### 3. Auditing System Calls (Syscalls)
To visualize the system calls performed by the helloworld binary, use the sequential and statistical statements of strace:

#### Chronological flow with timestamps
```bash
$ strace -tt ./helloworld
```
#### Statistical summary table of consumed syscalls
```bash
$ strace -c ./helloworld
```
---

## Authors
* Castilla, Pablo
* Blanco, Luciano Joaquin
* Bustamante, Marco Antonio

## Professors
* Solinas, Miguel Angel
* Jorge, Javier Alejandro
