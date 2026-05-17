Title: Introduction — The Linux Kernel  documentation
Mapped Topic: Kernel labs and lectures
Source URL: https://linux-kernel-labs.github.io/refs/heads/master/labs/introduction.html
Source Type: official_course_material
Trust Score: 95
Fetched At: 2026-04-17T07:06:17+00:00
Mapped From CSE.md Section: Part 2: C. Operating systems, Linux internals, kernel understanding

# Content

# Introduction[¶](https://linux-kernel-labs.github.io#introduction)

## Lab objectives[¶](https://linux-kernel-labs.github.io#lab-objectives)

- presenting the rules and objectives of the Operating Systems 2 lab
- introducing the lab documentation
- introducing the Linux kernel and related resources

## Keywords[¶](https://linux-kernel-labs.github.io#keywords)

- kernel, kernel programming
- Linux, vanilla,
[http://www.kernel.org](http://www.kernel.org) - cscope, LXR
- gdb, /proc/kcore, addr2line, dump_stack

## About this laboratory[¶](https://linux-kernel-labs.github.io#about-this-laboratory)

The Operating Systems 2 lab is a kernel programming and driver development lab. The objectives of the laboratory are:

- deepening the notions presented in the course
- presentation of kernel programming interfaces (kernel API)
- gaining documenting, development and debugging skills on a freestanding environment
- acquiring knowledge and skills for drivers development

A laboratory will present a set of concepts, applications and commands specific to a given problem. The lab will start with a presentation (each lab will have a set of slides) (15 minutes) and the remaining time will be allocated to the lab exercises (80 minutes).

For best laboratory performance, we recommend that you read the related slides. To fully understand a laboratory, we recommend going through the lab support. For in-depth study, use the supporting documentation.

## References[¶](https://linux-kernel-labs.github.io#references)

## Kernel Debugging[¶](https://linux-kernel-labs.github.io#kernel-debugging)

Debugging a kernel is a much more difficult process than the debugging of a program, because there is no support from the operating system. This is why this process is usually done using two computers, connected on serial interfaces.

### gdb (Linux)[¶](https://linux-kernel-labs.github.io#gdb-linux)

A simpler debug method on Linux, but with many disadvantages,
is local debugging, using [gdb](http://www.gnu.org/software/gdb/),
the uncompressed kernel image (`vmlinux`

) and `/proc/kcore`

(the real-time kernel image). This method is usually used to inspect
the kernel and detect certain inconsistencies while it runs. The
method is useful especially if the kernel was compiled using the
`-g`

option, which keeps debug information. Some well-known
debug techniques can't be used by this method, such as breakpoints
of data modification.

Note

Because `/proc`

is a virtual filesystem, `/proc/kcore`

does not physically exist on the disk. It is generated on-the-fly
by the kernel when a program tries to access `proc/kcore`

.

It is used for debugging purposes.

From **man proc**, we have:

```
/proc/kcore
This file represents the physical memory of the system and is stored in the ELF core file format. With this pseudo-file, and
an unstripped kernel (/usr/src/linux/vmlinux) binary, GDB can be used to examine the current state of any kernel data struc‐
tures.
```

The uncompressed kernel image offers information about the data structures and symbols it contains.

```
student@eg106$ cd ~/src/linux
student@eg106$ file vmlinux
vmlinux: ELF 32-bit LSB executable, Intel 80386, ...
student@eg106$ nm vmlinux | grep sys_call_table
c02e535c R sys_call_table
student@eg106$ cat System.map | grep sys_call_table
c02e535c R sys_call_table
```

The **nm** utility is used to show the symbols in an object or
executable file. In our case, `vmlinux`

is an ELF file. Alternately,
we can use the file `System.map`

to view information about the
symbols in kernel.

Then we use **gdb** to inspect the symbols using the uncompressed
kernel image. A simple **gdb** session is the following:

```
student@eg106$ cd ~/src/linux
stduent@eg106$ gdb --quiet vmlinux
Using host libthread_db library "/lib/tls/libthread_db.so.1".
(gdb) x/x 0xc02e535c
0xc02e535c `<sys_call_table>`: 0xc011bc58
(gdb) x/16 0xc02e535c
0xc02e535c `<sys_call_table>`: 0xc011bc58 0xc011482a 0xc01013d3 0xc014363d
0xc02e536c `<sys_call_table+16>`: 0xc014369f 0xc0142d4e 0xc0142de5 0xc011548b
0xc02e537c `<sys_call_table+32>`: 0xc0142d7d 0xc01507a1 0xc015042c 0xc0101431
0xc02e538c `<sys_call_table+48>`: 0xc014249e 0xc0115c6c 0xc014fee7 0xc0142725
(gdb) x/x sys_call_table
0xc011bc58 `<sys_restart_syscall>`: 0xffe000ba
(gdb) x/x &sys_call_table
0xc02e535c `<sys_call_table>`: 0xc011bc58
(gdb) x/16 &sys_call_table
0xc02e535c `<sys_call_table>`: 0xc011bc58 0xc011482a 0xc01013d3 0xc014363d
0xc02e536c `<sys_call_table+16>`: 0xc014369f 0xc0142d4e 0xc0142de5 0xc011548b
0xc02e537c `<sys_call_table+32>`: 0xc0142d7d 0xc01507a1 0xc015042c 0xc0101431
0xc02e538c `<sys_call_table+48>`: 0xc014249e 0xc0115c6c 0xc014fee7 0xc0142725
(gdb) x/x sys_fork
0xc01013d3 `<sys_fork>`: 0x3824548b
(gdb) disass sys_fork
Dump of assembler code for function sys_fork:
0xc01013d3 `<sys_fork+0>`: mov 0x38(%esp),%edx
0xc01013d7 `<sys_fork+4>`: mov $0x11,%eax
0xc01013dc `<sys_fork+9>`: push $0x0
0xc01013de `<sys_fork+11>`: push $0x0
0xc01013e0 `<sys_fork+13>`: push $0x0
0xc01013e2 `<sys_fork+15>`: lea 0x10(%esp),%ecx
0xc01013e6 `<sys_fork+19>`: call 0xc0111aab `<do_fork>`
0xc01013eb `<sys_fork+24>`: add $0xc,%esp
0xc01013ee `<sys_fork+27>`: ret
End of assembler dump.
```

It can be noticed that the uncompressed kernel image was used as an argument
for **gdb**. The image can be found in the root of the kernel sources
after compilation.

A few commands used for debugging using **gdb** are:

**x**(examine) - Used to show the contents of the memory area whose address is specified as an argument to the command (this address can be the value of a physical address, a symbol or the address of a symbol). It can take as arguments (preceded by`/`

): the format to display the data in (`x`

for hexadecimal,`d`

for decimal, etc.), how many memory units to display and the size of a memory unit.**disassemble**- Used to disassemble a function.**p**(print) - Used to evaluate and show the value of an expression. The format to show the data in can be specified as an argument (`/x`

for hexadecimal,`/d`

for decimal, etc.).

The analysis of the kernel image is a method of static analysis. If we
want to perform dynamic analysis (analyzing how the kernel runs, not
only its static image) we can use `/proc/kcore`

; this is a dynamic
image (in memory) of the kernel.

```
student@eg106$ gdb ~/src/linux/vmlinux /proc/kcore
Core was generated by `root=/dev/hda3 ro'.
#0 0x00000000 in ?? ()
(gdb) p sys_call_table
$1 = -1072579496
(gdb) p /x sys_call_table
$2 = 0xc011bc58
(gdb) p /x &sys_call_table
$3 = 0xc02e535c
(gdb) x/16 &sys_call_table
0xc02e535c `<sys_call_table>`: 0xc011bc58 0xc011482a 0xc01013d3 0xc014363d
0xc02e536c `<sys_call_table+16>`: 0xc014369f 0xc0142d4e 0xc0142de5 0xc011548b
0xc02e537c `<sys_call_table+32>`: 0xc0142d7d 0xc01507a1 0xc015042c 0xc0101431
0xc02e538c `<sys_call_table+48>`: 0xc014249e 0xc0115c6c 0xc014fee7 0xc0142725
```

Using the dynamic image of the kernel is useful for detecting [rootkits](http://en.wikipedia.org/wiki/Rootkit).

### Getting a stack trace[¶](https://linux-kernel-labs.github.io#getting-a-stack-trace)

Sometimes, you will want information about the trace the execution
reaches a certain point. You can determine this information using
**cscope** or LXR, but some function are called from many
execution paths, which makes this method difficult.

In these situations, it is useful to get a stack trace, which can be
simply done using the function `dump_stack()`

.

## Documentation[¶](https://linux-kernel-labs.github.io#documentation)

Kernel development is a difficult process, compared to user space programming. The API is different and the complexity of the subsystems in kernel requires additional preparation. The associated documentation is heterogeneous, sometimes requiring the inspection of multiple sources to have a more complete understanding of a certain aspect.

The main advantages of the Linux kernel are the access to sources and the open development system. Because of this, the Internet offers a larger number of documentation for the kernel.

A few links related to the Linux kernel are shown bellow:

[KernelNewbies](http://kernelnewbies.org)[KernelNewbies - Kernel Hacking](http://kernelnewbies.org/KernelHacking)[Kernel Analysis - HOWTO](http://www.tldp.org/HOWTO/KernelAnalysis-HOWTO.html)[Linux Kernel Programming](http://web.archive.org/web/20090228191439/http://www.linuxhq.com/lkprogram.html)[Linux kernel - Wikibooks](http://en.wikibooks.org/wiki/Linux_kernel)

The links are not comprehensive. Using [The Internet](http://www.google.com) and
[kernel source code](http://lxr.free-electrons.com/) is essential.

## Exercises[¶](https://linux-kernel-labs.github.io#exercises)

### Remarks[¶](https://linux-kernel-labs.github.io#remarks)

Note

- Usually, the steps used to develop a kernel module are the
following:
- editing the module source code (on the physical machine);
- module compilation (on the physical machine);
- generation of the minimal image for the virtual machine; this image contains the kernel, your module, busybox and eventually test programs;
- starting the virtual machine using QEMU;
- running the tests in the virtual machine.

- When using cscope, use
`~/src/linux`

. If there is no`cscope.out`

file, you can generate it using the command**make ARCH=x86 cscope**. - You can find more details about the virtual machine at
[Recommended Setup](https://linux-kernel-labs.github.io/info/vm.html#vm-link).

Important

Before solving an exercice, **carefully** read all its bullets.

### Booting the virtual machine[¶](https://linux-kernel-labs.github.io#booting-the-virtual-machine)

A summary of the virtual machine infrastructure:

`~/src/linux`

- Linux kernel sources, needed to compile modules. The directory contains the file`cscope.out`

, used for navigation in the source tree.`~/src/linux/tools/labs/qemu`

- scripts and auxiliary files used to generate and run the QEMU VM.

To start the VM, run **make boot** in the directory `~/src/linux/tools/labs`

:

```
student@eg106:~$ cd ~/src/linux/tools/labs
student@eg106:~/src/linux/tools/labs$ make boot
```

By default, you will not get a prompt or any graphical interface, but you can connect to
a console exposed by the virtual machine using **minicom** or **screen**.

```
student@eg106:~/src/linux/tools/labs$ minicom -D serial.pts
<press enter>
qemux86 login:
Poky (Yocto Project Reference Distro) 2.3 qemux86 /dev/hvc0
```

Alternatively, you can start the virtual machine with graphical interface support, using
the **QEMU_DISPLAY=gtk make boot**.

Note

To access the virtual machine, at the login prompt, enter the
username `root`

; there is no need to enter a password.
The virtual machine will start with the permissions of the
root account.

### Adding and using a virtual disk[¶](https://linux-kernel-labs.github.io#adding-and-using-a-virtual-disk)

Note

If you don't have the file `mydisk.img`

, you can download
it from the address [http://elf.cs.pub.ro/so2/res/laboratoare/mydisk.img](http://elf.cs.pub.ro/so2/res/laboratoare/mydisk.img).
The file must be placed in `tools/labs`

.

In the `~/src/linux/tools/labs`

directory, you have a new virtual
machine disk, in the file `mydisk.img`

. We want to add the disk
to the virtual machine and use it within the virtual machine.

Edit `qemu/Makefile`

and add `-drive file=mydisk.img,if=virtio,format=raw`

to the `QEMU_OPTS`

variable.

Note

There are already two disks added to qemu (disk1.img and disk2.img). You will need
to add the new one after them. In this case, the new disk can be accessed as
`/dev/vdd`

(vda is the root partition, vdb is disk1 and vdc is disk2).

Hint

You do not need to manually create the entry for the new disk in `/dev`

because the virtual machine uses **devtmpfs**.

Run `make`

in `tools/labs`

to boot the virtual machine.
Create `/test`

directory and try to mount the new disk:

```
mkdir /test
mount /dev/vdd /test
```

The reason why we can not mount the virtual disk is because we do not have support in the
kernel for the filesystem with which the `mydisk.img`

is formatted. You will need
to identify the filesystem for `mydisk.img`

and compile kernel support for that filesystem.

Close the virtual machine (close the QEMU window, you do not need to use another command).
Use the **file** command on the physical machine to find out with which filesystem
the `mydisk.img`

file is formatted. You will identify the **btrfs** file system.

You will need to enable **btrfs** support in the kernel and recompile the kernel image.

Warning

If you receive an error while executing the **make menuconfig**
command, you probably do not have the **libncurses5-dev**
package installed. Install it using the command:

```
sudo apt-get install libncurses5-dev
```

Hint

Enter the `~/src/linux/`

subdirectory. Run **make menuconfig**
and go to the *File systems* section. Enable *Btrfs filesystem support*.
You will need to use the builtin option (not the module), i.e. **<*>** must appear
next to the option (**not** **<M>**).

Save the configuration you have made. Use the default configuration file (`config`

).

In the kernel source subdirectory (`~/src/linux/`

) recompile using the command:

```
make
```

To wait less, you can use the **-j** option run multiple jobs in parallel.
Generally, it is recommended to use **number of CPUs+1**:

```
make -j5
```

After the kernel recompilation finishes, **restart** the QEMU virtual machine:
that is, launch the **make** command in the subdirectory. You
do not need to copy anything, because the `bzImage`

file is a symlink to the kernel
image you just recompiled.

Inside the QEMU virtual machine, repeat the **mkdir** and **mount** operations.
With support for the **btrfs** filesystem, now **mount** will finish successfully.

Note

When doing your homework, there is no need to recompile the kernel because you will only use kernel modules. However, it is important to be familiar with configuring and recompiling a kernel.

If you still plan to recompile the kernel, make a backup of the bzImage file (follow the link in ~/src/linux for the full path). This will allow you to return to the initial setup in order to have an environment identical to the one used by vmchecker.

### GDB and QEMU[¶](https://linux-kernel-labs.github.io#gdb-and-qemu)

We can investigate and troubleshoot the QEMU virtual machine in real time.

Note

You can also use the **GDB Dashboard** plugin for a user-friendly interface.
**gdb** must be compiled with Python support.

In order to install it, you can just run:

```
wget -P ~ git.io/.gdbinit
```

To do this, we start the QEMU virtual machine first. Then, we can connect
with **gdb** to **a running QEMU virtual machine** using the command

```
make gdb
```

We used the QEMU command with the **-s** parameter, which means
listening to port `1234`

from **gdb**. We can do debugging
using a **remote target** for **gdb**. The existing `Makefile`

takes care of the details.

When you attach a debugger to a process, the process is suspended. You can add breakpoints and inspect the current status of the process.

Attach to the QEMU virtual machine (using the **make gdb** command)
and place a breakpoint in the `sys_access`

function using the
following command in the **gdb** console:

```
break sys_access
```

At this time, the virtual machine is suspended. To continue executing it (up to the possible call
of the `sys_access`

function), use the command:

```
continue
```

in the **gdb** console.

At this time, the virtual machine is active and has a usable console.
To make a `sys_access`

call, issue a **ls** command.
Note that the virtual machine was again suspended by **gdb**
and the corresponding `sys_access`

callback message appeared within the **gdb** console.

Trace code execution using **step** instruction, **continue** or **next**
instruction. You probably do not understand everything that happens, so use commands
such as **list** and **backtrace** to trace the execution.

Hint

At the **gdb** prompt, you can press **Enter**
(without anything else) to rerun the last command.

### 4. GDB spelunking[¶](https://linux-kernel-labs.github.io#gdb-spelunking)

Use **gdb** to display the source code of the function that creates kernel threads
(`kernel_thread`

).

Note

You can use GDB for static kernel analysis using, in the kernel source directory, a command such as:

```
gdb vmlinux
```

Go over the [gdb (Linux)](https://linux-kernel-labs.github.io#gdb-linux) section of the lab.

Use **gdb** to find the address of the `jiffies`

variable in memory and its contents.
The `jiffies`

variable holds the number of ticks (clock beats) since the system started.

Hint

To track the value of the jiffies variable, use dynamic analysis in **gdb**
by running the command:

```
make gdb
```

as in the previous exercise.

Go over the [gdb (Linux)](https://linux-kernel-labs.github.io#gdb-linux) section of the lab.

Hint

The `jiffies`

is a 64-bit variable.
You can see that its address is the same as the `jiffies_64`

variable.

To explore the contents of a 64-bit variable, use in the **gdb** console the command:

```
x/gx & jiffies
```

If you wanted to display the contents of the 32-bit variable,
you would use in the **gdb** console the command:

```
x/wx & jiffies
```

### 5. Cscope spelunking[¶](https://linux-kernel-labs.github.io#cscope-spelunking)

Use LXR or cscope in the `~/src/linux/`

directory to discover
the location of certain structures or functions.

Cscope index files are already generated. Use **vim** and other related commands
to scroll through the source code. For example, use the command:

```
vim
```

for opening the **vim** editor. Afterwards, inside the editor, use commands such as:

**:cs find g task_struct**.

Find the file in which the following data types are defined:

`struct task_struct`

`struct semaphore`

`struct list_head`

`spinlock_t`

`struct file_system_type`

Hint

For a certain structure, only its name needs to be searched.

For instance, in the case of **struct task_struct**,
search for the **task_struct** string.

Usually, you will get more matches. To locate the one you are interested in, do the following:

- List all matches by using, in
**vim**,**:copen**command. - Look for the right match (where the structure is defined) by looking for an open character
(
**{**), a single character on the structure definition line. To search for the open braid you use in**vim**the construction**/{**. - On the respective line, press
**Enter**to get into the source code where the variable is defined. - Close the secondary window using the command:
**:cclose**command.

Find the file in which the following global kernel variables are declared:

`sys_call_table`

`file_systems`

`current`

`chrdevs`

Hint

To do this, use a **vim** command with the syntax:

**:cs f g <symbol>**

where **<symbol>** is the name of the symbol being searched.

Find the file in which the following functions are declared:

`copy_from_user`

`vmalloc`

`schedule_timeout`

`add_timer`

Hint

To do this, use a **vim** command with the syntax:

**:cs f g <symbol>**

where **<symbol>** is the name of the symbol being searched.

Scroll through the following sequence of structures:

`struct task_struct`

`struct mm_struct`

`struct vm_area_struct`

`struct vm_operations_struct`

That is, you access a structure and then you find fields with the data type of the next structure, access the respective fields and so on. Note in which files these structures are defined; this will be useful to the following labs.

Hint

In order to search for a symbol in **vim** (with **cscope** support)
when the cursor is placed on it, use the **Ctrl+]** keyboard shortcut.

To return to the previous match (the one before search/jump), use the
**Ctrl+o** keyboard shortcut.

To move forward with the search (to return to matches before **Ctrl+o**),
use the **Ctrl+i** keyboard shortcut.

Following the above instructions, find and go through the function call sequence:

`bio_alloc`

`bio_alloc_bioset`

`bvec_alloc`

`kmem_cache_alloc`

`slab_alloc`

Note

Read [cscope](https://linux-kernel-labs.github.io#cscope) or [LXR Cross-Reference](https://linux-kernel-labs.github.io#lxr-cross-reference) sections of the lab.
