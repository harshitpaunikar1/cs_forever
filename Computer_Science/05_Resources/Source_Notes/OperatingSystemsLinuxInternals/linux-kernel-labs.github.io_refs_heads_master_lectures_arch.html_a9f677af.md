Title: Architecture Layer — The Linux Kernel  documentation
Mapped Topic: Kernel labs and lectures
Source URL: https://linux-kernel-labs.github.io/refs/heads/master/lectures/arch.html
Source Type: official_course_material
Trust Score: 95
Fetched At: 2026-04-17T07:06:24+00:00
Mapped From CSE.md Section: Part 2: C. Operating systems, Linux internals, kernel understanding

# Content

# Architecture Layer[¶](https://linux-kernel-labs.github.io#architecture-layer)

## Lecture objectives:[¶](https://linux-kernel-labs.github.io#lecture-objectives)

- Overview of the arch layer
- Overview of the boot process

## Overview of the arch layer[¶](https://linux-kernel-labs.github.io#overview-of-the-arch-layer)

### Boot strap[¶](https://linux-kernel-labs.github.io#boot-strap)

- The first kernel code that runs
- Typically runs with the MMU disabled
- Move / Relocate kernel code

### Boot strap[¶](https://linux-kernel-labs.github.io#boot-strap-1)

- The first kernel code that runs
- Typically runs with the MMU disabled
- Copy bootloader arguments and determine kernel run location
- Move / relocate kernel code to final location
- Initial MMU setup - map the kernel

### Memory setup[¶](https://linux-kernel-labs.github.io#memory-setup)

- Determine available memory and setup the boot memory allocator
- Manages memory regions before the page allocator is setup
- Bootmem - used a bitmap to track free blocks
- Memblock - deprecates bootmem and adds support for memory ranges
- Supports both physical and virtual addresses
- support NUMA architectures

### MMU management[¶](https://linux-kernel-labs.github.io#mmu-management)

- Implements the generic page table manipulation APIs: types, accessors, flags
- Implement TLB management APIs: flush, invalidate

### Thread Management[¶](https://linux-kernel-labs.github.io#thread-management)

- Defines the thread type (struct thread_info) and implements functions for allocating threads (if needed)
- Implement
`copy_thread()`

and`switch_context()`

### Time Management[¶](https://linux-kernel-labs.github.io#time-management)

- Setup the timer tick and provide a time source
- Mostly transitioned to platform drivers
- clock_event_device - for scheduling timers
- clocksource - for reading the time

### IRQs and exception management[¶](https://linux-kernel-labs.github.io#irqs-and-exception-management)

- Define interrupt and exception handlers / entry points
- Setup priorities
- Platform drivers for interrupt controllers

### System calls[¶](https://linux-kernel-labs.github.io#system-calls)

- Define system call entry point(s)
- Implement user-space access primitives (e.g. copy_to_user)

### Platform Drivers[¶](https://linux-kernel-labs.github.io#platform-drivers)

- Platform and architecture specific drivers
- Bindings to platform device enumeration methods (e.g. device tree or ACPI)

### Machine specific code[¶](https://linux-kernel-labs.github.io#machine-specific-code)

- Some architectures use a "machine" / "platform" abstraction
- Typical for architecture used in embedded systems with a lot of variety (e.g. ARM, powerPC)
