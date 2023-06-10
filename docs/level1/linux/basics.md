# Linux Basics

## Introduction


## What to expect from this course

Fundamentals of Linux operating systems: Covers Linux architecture, distributions, and various uses. Explains the difference between GUI and CLI.

Basic Linux commands: Focuses on navigating the file system, manipulating files, and using I/O redirection.

Linux system administration: Covers tasks performed by Linux admins, such as managing users/groups, file permissions, monitoring system performance, and working with log files.

## What are Linux operating systems

Linux operating systems are a family of open-source operating systems based on the Linux kernel. They are known for their stability, security, and flexibility. Linux distributions, also known as "distros," are different variants of Linux that are customized and packaged with various software applications, tools, and desktop environments. Some popular Linux operating systems include Ubuntu, Fedora, Debian, CentOS, and Arch Linux. These operating systems are widely used in servers, desktop computers, embedded systems, and other devices.

A kernel is the most important part of an operating system - it performs important functions like process management, memory management, filesystem management etc.

## What are popular Linux distributions

A Linux distribution(distro) is an operating system based on
the Linux kernel and a package management system. A package management
system consists of tools that help in installing, upgrading,
configuring and removing softwares on the operating system.

Software are usually adopted to a distribution and are packaged in a
distro specific format. These packages are available through a distro
specific repository. Packages are installed and managed in the operating
system by a package manager.

** Popular Linux distributions: **

- Fedora

- Ubuntu

- Debian

- Centos

- Red Hat Enterprise Linux

- Suse

- Arch Linux

## Linux Architecture

- **The Linux kernel is monolithic in nature.**
    - The Linux kernel is designed as a monolithic kernel, which means that the entire operating system kernel is present and runs in a single address space. This design allows for efficient communication and sharing of data between different kernel components. However, it also means that any issue or bug within the kernel can potentially affect the stability and security of the entire system.

- **System calls are used to interact with the Linux kernel space.**
    - System calls are the interface between user space and kernel space in Linux. They provide a way for user programs to request services from the kernel, such as file operations, process management, and device control. When a user program needs to perform a privileged operation or access hardware resources, it makes a system call, which transfers control from user space to kernel space.

- **Kernel code can only be executed in the kernel mode. Non-kernel code is executed in the user mode.**
    - The Linux kernel enforces a separation between kernel mode and user mode. Kernel code runs in a privileged mode called kernel mode, where it has direct access to system resources and can execute privileged instructions. On the other hand, non-kernel code, such as user programs, runs in user mode, which restricts their access to system resources and ensures protection and isolation.

- **Device drivers are used to communicate with the hardware devices.**
    - Device drivers are software components that facilitate communication between the operating system and hardware devices. In the Linux ecosystem, device drivers are used to control and manage various hardware components, such as network cards, graphics cards, storage devices, and input/output devices. They provide an abstraction layer that allows the operating system to interact with the specific functionalities and features of each hardware device, enabling proper utilization and integration of hardware resources within the system.



