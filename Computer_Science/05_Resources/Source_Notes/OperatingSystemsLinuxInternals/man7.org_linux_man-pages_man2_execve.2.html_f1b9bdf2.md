Title: execve(2) - Linux manual page
Mapped Topic: Linux systems programming interfaces
Source URL: https://man7.org/linux/man-pages/man2/execve.2.html
Source Type: official_reference
Trust Score: 96
Fetched At: 2026-04-17T07:05:30+00:00
Mapped From CSE.md Section: Part 2: C. Operating systems, Linux internals, kernel understanding

# Content

|
|
|
|
|

```
```*execve*(2) System Calls Manual *execve*(2)

execve - execute program

Standard C library (libc,-lc)

#include <unistd.h>int execve(const char *path, char *const _Nullableargv[],char *const _Nullableenvp[]);

execve() executes the program referred to bypath. This causes the program that is currently being run by the calling process to be replaced with a new program, with newly initialized stack, heap, and (initialized and uninitialized) data segments.pathmust be either a binary executable, or a script starting with a line of the form:#!interpreter[optional-arg] For details of the latter case, see "Interpreter scripts" below.argvis an array of pointers to strings passed to the new program as its command-line arguments. By convention, the first of these strings (i.e.,argv[0]) should contain the filename associated with the file being executed. Theargvarray must be terminated by a null pointer. (Thus, in the new program,argv[argc]will be a null pointer.)envpis an array of pointers to strings, conventionally of the formkey=value, which are passed as the environment of the new program. Theenvparray must be terminated by a null pointer. This manual page describes the Linux system call in detail; for an overview of the nomenclature and the many, often preferable, standardised variants of this function provided by libc, including ones that search thePATHenvironment variable, see[exec(3)]. The argument vector and environment can be accessed by the new program's main function, when it is defined as: int main(int argc, char *argv[], char *envp[]) Note, however, that the use of a third argument to the main function is not specified in POSIX.1; according to POSIX.1, the environment should be accessed via the external variable[environ(7)].execve() does not return on success, and the text, initialized data, uninitialized data (bss), and stack of the calling process are overwritten according to the contents of the newly loaded program. If the current program is being ptraced, aSIGTRAPsignal is sent to it after a successfulexecve(). If the set-user-ID bit is set on the program file referred to bypath, then the effective user ID of the calling process is changed to that of the owner of the program file. Similarly, if the set- group-ID bit is set on the program file, then the effective group ID of the calling process is set to the group of the program file. The aforementioned transformations of the effective IDs arenotperformed (i.e., the set-user-ID and set-group-ID bits are ignored) if any of the following is true: â¢ theno_new_privsattribute is set for the calling thread (see[prctl(2)]); â¢ the underlying filesystem is mountednosuid(theMS_NOSUIDflag for[mount(2)]); or â¢ the calling process is being ptraced. The capabilities of the program file (see[capabilities(7)]) are also ignored if any of the above are true. The effective user ID of the process is copied to the saved set- user-ID; similarly, the effective group ID is copied to the saved set-group-ID. This copying takes place after any effective ID changes that occur because of the set-user-ID and set-group-ID mode bits. The process's real UID and real GID, as well as its supplementary group IDs, are unchanged by a call toexecve(). If the executable is an a.out dynamically linked binary executable containing shared-library stubs, the Linux dynamic linker[ld.so(8)]is called at the start of execution to bring needed shared objects into memory and link the executable with them. If the executable is a dynamically linked ELF executable, the interpreter named in the PT_INTERP segment is used to load the needed shared objects. This interpreter is typically/lib/ld-linux.so.2for binaries linked with glibc (see[ld-linux.so(8)]).Effect on process attributesAll process attributes are preserved during anexecve(), except the following: â¢ The dispositions of any signals that are being caught are reset to the default ([signal(7)]). â¢ Any alternate signal stack is not preserved ([sigaltstack(2)]). â¢ Memory mappings are not preserved ([mmap(2)]). â¢ Attached System V shared memory segments are detached ([shmat(2)]). â¢ POSIX shared memory regions are unmapped ([shm_open(3)]). â¢ Open POSIX message queue descriptors are closed ([mq_overview(7)]). â¢ Any open POSIX named semaphores are closed ([sem_overview(7)]). â¢ POSIX timers are not preserved ([timer_create(2)]). â¢ Any open directory streams are closed ([opendir(3)]). â¢ Memory locks are not preserved ([mlock(2)],[mlockall(2)]). â¢ Exit handlers are not preserved ([atexit(3)],[on_exit(3)]). â¢ The floating-point environment is reset to the default (see[fenv(3)]). The process attributes in the preceding list are all specified in POSIX.1. The following Linux-specific process attributes are also not preserved during anexecve(): â¢ The process's "dumpable" attribute is set to the value 1, unless a set-user-ID program, a set-group-ID program, or a program with capabilities is being executed, in which case the dumpable flag may instead be reset to the value in/proc/sys/fs/suid_dumpable, in the circumstances described underPR_SET_DUMPABLEin[prctl(2)]. Note that changes to the "dumpable" attribute may cause ownership of files in the process's/proc/pid directory to change toroot:root, as described in[proc(5)]. â¢ The[prctl(2)]PR_SET_KEEPCAPSflag is cleared. â¢ (Since Linux 2.4.36 / 2.6.23) If a set-user-ID or set-group-ID program is being executed, then the parent death signal set by[prctl(2)]PR_SET_PDEATHSIGflag is cleared. â¢ The process name, as set by[prctl(2)]PR_SET_NAME(and displayed byps -o comm), is reset to the name of the new executable file. â¢ TheSECBIT_KEEP_CAPSsecurebitsflag is cleared. See[capabilities(7)]. â¢ The termination signal is reset toSIGCHLD(see[clone(2)]). â¢ The file descriptor table is unshared, undoing the effect of theCLONE_FILESflag of[clone(2)]. Note the following further points: â¢ All threads other than the calling thread are destroyed during anexecve(). Mutexes, condition variables, and other pthreads objects are not preserved. â¢ The equivalent ofsetlocale(LC_ALL, "C")is executed at program start-up. â¢ POSIX.1 specifies that the dispositions of any signals that are ignored or set to the default are left unchanged. POSIX.1 specifies one exception: ifSIGCHLDis being ignored, then an implementation may leave the disposition unchanged or reset it to the default; Linux does the former. â¢ Any outstanding asynchronous I/O operations are canceled ([aio_read(3)],[aio_write(3)]). â¢ For the handling of capabilities duringexecve(), see[capabilities(7)]. â¢ By default, file descriptors remain open across anexecve(). File descriptors that are marked close-on-exec are closed; see the description ofFD_CLOEXECin[fcntl(2)]. (If a file descriptor is closed, this will cause the release of all record locks obtained on the underlying file by this process. See[fcntl(2)]for details.) POSIX.1 says that if file descriptors 0, 1, and 2 would otherwise be closed after a successfulexecve(), and the process would gain privilege because the set- user-ID or set-group-ID mode bit was set on the executed file, then the system may open an unspecified file for each of these file descriptors. As a general principle, no portable program, whether privileged or not, can assume that these three file descriptors will remain closed across anexecve().Interpreter scriptsAn interpreter script is a text file that has execute permission enabled and whose first line is of the form:#!interpreter[optional-arg] Theinterpretermust be a valid pathname for an executable file.interpreterwill be invoked with the following arguments:interpreter[optional-arg]path arg... wherearg...is the series of words pointed to by theargvargument ofexecve(), starting atargv[1]. Note that there is no way to get theargv[0]that was passed to theexecve() call. For portable use,optional-argshould either be absent, or be specified as a single word (i.e., it should not contain white space); see VERSIONS below. Since Linux 2.6.28, the kernel permits the interpreter of a script to itself be a script. This permission is recursive, up to a limit of four recursions, so that the interpreter may be a script which is interpreted by a script, and so on.Limits on size of arguments and environmentMost UNIX implementations impose some limit on the total size of the command-line argument (argv) and environment (envp) strings that may be passed to a new program. POSIX.1 allows an implementation to advertise this limit using theARG_MAXconstant (either defined in<limits.h>or available at run time using the callsysconf(_SC_ARG_MAX)). Before Linux 2.6.23, the memory used to store the environment and argument strings was limited to 32 pages (defined by the kernel constantMAX_ARG_PAGES). On architectures with a 4-kB page size, this yields a maximum size of 128 kB. On Linux 2.6.23 and later, most architectures support a size limit derived from the softRLIMIT_STACKresource limit (see[getrlimit(2)]) that is in force at the time of theexecve() call. (Architectures with no memory management unit are excepted: they maintain the limit that was in effect before Linux 2.6.23.) This change allows programs to have a much larger argument and/or environment list. For these architectures, the total size is limited to 1/4 of the allowed stack size. (Imposing the 1/4-limit ensures that the new program always has some stack space.) Additionally, the total size is limited to 3/4 of the value of the kernel constant_STK_LIM(8 MiB). Since Linux 2.6.25, the kernel also places a floor of 32 pages on this size limit, so that, even whenRLIMIT_STACKis set very low, applications are guaranteed to have at least as much argument and environment space as was provided by Linux 2.6.22 and earlier. (This guarantee was not provided in Linux 2.6.23 and 2.6.24.) Additionally, the limit per string is 32 pages (the kernel constantMAX_ARG_STRLEN), and the maximum number of strings is 0x7FFFFFFF.

On success,execve() does not return, on error -1 is returned, andis set to indicate the error.[errno]

E2BIGThe total number of bytes in the environment (envp) and argument list (argv) is too large, an argument or environment string is too long, or the fullpathof the executable is too long. The terminating null byte is counted as part of the string length.EACCESSearch permission is denied on a component of the path prefix ofpathor the name of a script interpreter. (See also[path_resolution(7)].)EACCESThe file or a script interpreter is not a regular file.EACCESExecute permission is denied for the file or a script or ELF interpreter.EACCESThe filesystem is mountednoexec.EAGAIN(since Linux 3.1) Having changed its real UID using one of theset*uid() calls, the caller wasâand is now stillâabove itsRLIMIT_NPROCresource limit (see[setrlimit(2)]). For a more detailed explanation of this error, see NOTES.EFAULTpathor one of the pointers in the vectorsargvorenvppoints outside your accessible address space.EINVALAn ELF executable had more than one PT_INTERP segment (i.e., tried to name more than one interpreter).EIOAn I/O error occurred.EISDIRAn ELF interpreter was a directory.ELIBBADAn ELF interpreter was not in a recognized format.ELOOPToo many symbolic links were encountered in resolvingpathor the name of a script or ELF interpreter.ELOOPThe maximum recursion limit was reached during recursive script interpretation (see "Interpreter scripts", above). Before Linux 3.8, the error produced for this case wasENOEXEC.EMFILEThe per-process limit on the number of open file descriptors has been reached.ENAMETOOLONGpathis too long.ENFILEThe system-wide limit on the total number of open files has been reached.ENOENTpathor a script or ELF interpreter does not exist.ENOEXECAn executable is not in a recognized format, is for the wrong architecture, or has some other format error that means it cannot be executed.ENOMEMInsufficient kernel memory was available.ENOTDIRA component of the path prefix ofpathor a script or ELF interpreter is not a directory.EPERMThe filesystem is mountednosuid, the user is not the superuser, and the file has the set-user-ID or set-group-ID bit set.EPERMThe process is being traced, the user is not the superuser and the file has the set-user-ID or set-group-ID bit set.EPERMA "capability-dumb" applications would not obtain the full set of permitted capabilities granted by the executable file. See[capabilities(7)].ETXTBSYThe specified executable was open for writing by one or more processes.

POSIX does not document the #! behavior, but it exists (with some variations) on other UNIX systems. On Linux,argvandenvpcan be specified as NULL. In both cases, this has the same effect as specifying the argument as a pointer to a list containing a single null pointer.Do not take advantageof this nonstandard and nonportable misfeature!On many other UNIX systems, specifyingargvas NULL will result in an error (EFAULT).Someother UNIX systems treat theenvp==NULLcase the same as Linux. POSIX.1 says that values returned by[sysconf(3)]should be invariant over the lifetime of a process. However, since Linux 2.6.23, if theRLIMIT_STACKresource limit changes, then the value reported by_SC_ARG_MAXwill also change, to reflect the fact that the limit on space for holding command-line arguments and environment variables has changed.Interpreter scriptsThe kernel imposes a maximum length on the text that follows the "#!" characters at the start of a script; characters beyond the limit are ignored. Before Linux 5.1, the limit is 127 characters. Since Linux 5.1, the limit is 255 characters. The semantics of theoptional-argargument of an interpreter script vary across implementations. On Linux, the entire string following theinterpretername is passed as a single argument to the interpreter, and this string can include white space. However, behavior differs on some other systems. Some systems use the first white space to terminateoptional-arg. On some systems, an interpreter script can have multiple arguments, and white spaces inoptional-argare used to delimit the arguments. Linux (like most other modern UNIX systems) ignores the set-user- ID and set-group-ID bits on scripts.

POSIX.1-2024.

POSIX.1-2001, SVr4, 4.3BSD. With UNIX V6, the argument list of anexec() call was ended by 0, while the argument list ofmainwas ended by -1. Thus, this argument list was not directly usable in a furtherexec() call. Since UNIX V7, both are NULL.

One sometimes seesexecve() (and the related functions described in[exec(3)]) described as "executing anewprocess" (or similar). This is a highly misleading description: there is no new process; many attributes of the calling process remain unchanged (in particular, its PID). All thatexecve() does is arrange for an existing process (the calling process) to execute a new program. Set-user-ID and set-group-ID processes can not be[ptrace(2)]d. The result of mounting a filesystemnosuidvaries across Linux kernel versions: some will refuse execution of set-user-ID and set-group-ID executables when this would give the user powers they did not have already (and returnEPERM), some will just ignore the set-user-ID and set-group-ID bits andexec() successfully. In most cases whereexecve() fails, control returns to the original executable image, and the caller ofexecve() can then handle the error. However, in (rare) cases (typically caused by resource exhaustion), failure may occur past the point of no return: the original executable image has been torn down, but the new image could not be completely built. In such cases, the kernel kills the process with aSIGSEGV(SIGKILLuntil Linux 3.17) signal.execve() and EAGAINA more detailed explanation of theEAGAINerror that can occur (since Linux 3.1) when callingexecve() is as follows. TheEAGAINerror can occur when aprecedingcall to[setuid(2)],[setreuid(2)], or[setresuid(2)]caused the real user ID of the process to change, and that change caused the process to exceed itsRLIMIT_NPROCresource limit (i.e., the number of processes belonging to the new real UID exceeds the resource limit). From Linux 2.6.0 to Linux 3.0, this caused theset*uid() call to fail. (Before Linux 2.6, the resource limit was not imposed on processes that changed their user IDs.) Since Linux 3.1, the scenario just described no longer causes theset*uid() call to fail, because it too often led to security holes where buggy applications didn't check the return status and assumed thatâif the caller had root privilegesâthe call would always succeed. Instead, theset*uid() calls now successfully change the real UID, but the kernel sets an internal flag, namedPF_NPROC_EXCEEDED, to note that theRLIMIT_NPROCresource limit has been exceeded. If thePF_NPROC_EXCEEDEDflag is set and the resource limit is still exceeded at the time of a subsequentexecve() call, that call fails with the errorEAGAIN. This kernel logic ensures that theRLIMIT_NPROCresource limit is still enforced for the common privileged daemon workflowânamely,[fork(2)]+set*uid() +execve(). If the resource limit was not still exceeded at the time of theexecve() call (because other processes belonging to this real UID terminated between theset*uid() call and theexecve() call), then theexecve() call succeeds and the kernel clears thePF_NPROC_EXCEEDEDprocess flag. The flag is also cleared if a subsequent call to[fork(2)]by this process succeeds.

The following program is designed to be execed by the second program below. It just echoes its command-line arguments, one per line. /* myecho.c */ #include <stdio.h> #include <stdlib.h> int main(int argc, char *argv[]) { for (size_t j = 0; j < argc; j++) printf("argv[%zu]: %s\n", j, argv[j]); exit(EXIT_SUCCESS); } This program can be used to exec the program named in its command- line argument: /* execve.c */ #include <stdio.h> #include <stdlib.h> #include <unistd.h> int main(int argc, char *argv[]) { static char *newargv[] = { NULL, "hello", "world", NULL }; static char *newenviron[] = { NULL }; if (argc != 2) { fprintf(stderr, "Usage: %s <file-to-exec>\n", argv[0]); exit(EXIT_FAILURE); } newargv[0] = argv[1]; execve(argv[1], newargv, newenviron); perror("execve"); /* execve() returns only on error */ exit(EXIT_FAILURE); } We can use the second program to exec the first as follows: $cc myecho.c -o myecho$cc execve.c -o execve$./execve ./myechoargv[0]: ./myecho argv[1]: hello argv[2]: world We can also use these programs to demonstrate the use of a script interpreter. To do this we create a script whose "interpreter" is ourmyechoprogram: $cat > script#!./myecho script-arg^D$chmod +x scriptWe can then use our program to exec the script: $./execve ./scriptargv[0]: ./myecho argv[1]: script-arg argv[2]: ./script argv[3]: hello argv[4]: world

[chmod(2)],[execveat(2)],[fork(2)],[get_robust_list(2)],[ptrace(2)],[exec(3)],[fexecve(3)],[getauxval(3)],[getopt(3)],[system(3)],[capabilities(7)],[credentials(7)],[environ(7)],[path_resolution(7)],[ld.so(8)]

This page is part of theman-pages(Linux kernel and C library user-space interface documentation) project. Information about the project can be found at â¨[https://www.kernel.org/doc/man-pages/]â©. If you have a bug report for this manual page, see â¨[https://git.kernel.org/pub/scm/docs/man-pages/man-pages.git/tree/CONTRIBUTING]â©. This page was obtained from the tarball man-pages-6.16.tar.gz fetched from â¨[https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/]â© on 2026-01-16. If you discover any rendering problems in this HTML version of the page, or you believe there is a better or more up- to-date source for the page, or you have corrections or improvements to the information in this COLOPHON (which isnotpart of the original manual page), send a mail to man-pages@man7.org Linux man-pages 6.16 2025-10-29execve(2)

Pages that refer to this page:
[pmcd(1)](https://man7.org/man1/pmcd.1.html),
[setpriv(1)](https://man7.org/man1/setpriv.1.html),
[strace(1)](https://man7.org/man1/strace.1.html),
[access(2)](https://man7.org/man2/access.2.html),
[alarm(2)](https://man7.org/man2/alarm.2.html),
[arch_prctl(2)](https://man7.org/man2/arch_prctl.2.html),
[brk(2)](https://man7.org/man2/brk.2.html),
[chdir(2)](https://man7.org/man2/chdir.2.html),
[chmod(2)](https://man7.org/man2/chmod.2.html),
[chroot(2)](https://man7.org/man2/chroot.2.html),
[clone(2)](https://man7.org/man2/clone.2.html),
[close(2)](https://man7.org/man2/close.2.html),
[eventfd(2)](https://man7.org/man2/eventfd.2.html),
[execveat(2)](https://man7.org/man2/execveat.2.html),
[_exit(2)](https://man7.org/man2/_exit.2.html),
[fanotify_mark(2)](https://man7.org/man2/fanotify_mark.2.html),
[fcntl_locking(2)](https://man7.org/man2/fcntl_locking.2.html),
[F_GETFD(2const)](https://man7.org/man2/F_GETFD.2const.html),
[flock(2)](https://man7.org/man2/flock.2.html),
[fork(2)](https://man7.org/man2/fork.2.html),
[getgroups(2)](https://man7.org/man2/getgroups.2.html),
[getitimer(2)](https://man7.org/man2/getitimer.2.html),
[getpriority(2)](https://man7.org/man2/getpriority.2.html),
[getrlimit(2)](https://man7.org/man2/getrlimit.2.html),
[get_robust_list(2)](https://man7.org/man2/get_robust_list.2.html),
[getrusage(2)](https://man7.org/man2/getrusage.2.html),
[ioctl(2)](https://man7.org/man2/ioctl.2.html),
[ioctl_console(2)](https://man7.org/man2/ioctl_console.2.html),
[ioperm(2)](https://man7.org/man2/ioperm.2.html),
[iopl(2)](https://man7.org/man2/iopl.2.html),
[KEYCTL_SET_REQKEY_KEYRING(2const)](https://man7.org/man2/KEYCTL_SET_REQKEY_KEYRING.2const.html),
[madvise(2)](https://man7.org/man2/madvise.2.html),
[memfd_create(2)](https://man7.org/man2/memfd_create.2.html),
[memfd_secret(2)](https://man7.org/man2/memfd_secret.2.html),
[mlock(2)](https://man7.org/man2/mlock.2.html),
[mount(2)](https://man7.org/man2/mount.2.html),
[open(2)](https://man7.org/man2/open.2.html),
[perf_event_open(2)](https://man7.org/man2/perf_event_open.2.html),
[personality(2)](https://man7.org/man2/personality.2.html),
[PR_CAPBSET_READ(2const)](https://man7.org/man2/PR_CAPBSET_READ.2const.html),
[PR_GET_NO_NEW_PRIVS(2const)](https://man7.org/man2/PR_GET_NO_NEW_PRIVS.2const.html),
[PR_GET_SPECULATION_CTRL(2const)](https://man7.org/man2/PR_GET_SPECULATION_CTRL.2const.html),
[PR_MPX_ENABLE_MANAGEMENT(2const)](https://man7.org/man2/PR_MPX_ENABLE_MANAGEMENT.2const.html),
[PR_PAC_RESET_KEYS(2const)](https://man7.org/man2/PR_PAC_RESET_KEYS.2const.html),
[PR_SET_CHILD_SUBREAPER(2const)](https://man7.org/man2/PR_SET_CHILD_SUBREAPER.2const.html),
[PR_SET_DUMPABLE(2const)](https://man7.org/man2/PR_SET_DUMPABLE.2const.html),
[PR_SET_IO_FLUSHER(2const)](https://man7.org/man2/PR_SET_IO_FLUSHER.2const.html),
[PR_SET_KEEPCAPS(2const)](https://man7.org/man2/PR_SET_KEEPCAPS.2const.html),
[PR_SET_NO_NEW_PRIVS(2const)](https://man7.org/man2/PR_SET_NO_NEW_PRIVS.2const.html),
[PR_SET_PDEATHSIG(2const)](https://man7.org/man2/PR_SET_PDEATHSIG.2const.html),
[PR_SET_SPECULATION_CTRL(2const)](https://man7.org/man2/PR_SET_SPECULATION_CTRL.2const.html),
[PR_SET_SYSCALL_USER_DISPATCH(2const)](https://man7.org/man2/PR_SET_SYSCALL_USER_DISPATCH.2const.html),
[PR_SET_TAGGED_ADDR_CTRL(2const)](https://man7.org/man2/PR_SET_TAGGED_ADDR_CTRL.2const.html),
[PR_SET_THP_DISABLE(2const)](https://man7.org/man2/PR_SET_THP_DISABLE.2const.html),
[PR_SET_TIMERSLACK(2const)](https://man7.org/man2/PR_SET_TIMERSLACK.2const.html),
[PR_SVE_GET_VL(2const)](https://man7.org/man2/PR_SVE_GET_VL.2const.html),
[PR_SVE_SET_VL(2const)](https://man7.org/man2/PR_SVE_SET_VL.2const.html),
[ptrace(2)](https://man7.org/man2/ptrace.2.html),
[sched_setaffinity(2)](https://man7.org/man2/sched_setaffinity.2.html),
[seccomp(2)](https://man7.org/man2/seccomp.2.html),
[semop(2)](https://man7.org/man2/semop.2.html),
[set_mempolicy(2)](https://man7.org/man2/set_mempolicy.2.html),
[setpgid(2)](https://man7.org/man2/setpgid.2.html),
[setresuid(2)](https://man7.org/man2/setresuid.2.html),
[setreuid(2)](https://man7.org/man2/setreuid.2.html),
[setsid(2)](https://man7.org/man2/setsid.2.html),
[setuid(2)](https://man7.org/man2/setuid.2.html),
[shmop(2)](https://man7.org/man2/shmop.2.html),
[sigaction(2)](https://man7.org/man2/sigaction.2.html),
[sigaltstack(2)](https://man7.org/man2/sigaltstack.2.html),
[signalfd(2)](https://man7.org/man2/signalfd.2.html),
[sigpending(2)](https://man7.org/man2/sigpending.2.html),
[sigprocmask(2)](https://man7.org/man2/sigprocmask.2.html),
[syscalls(2)](https://man7.org/man2/syscalls.2.html),
[timer_create(2)](https://man7.org/man2/timer_create.2.html),
[timerfd_create(2)](https://man7.org/man2/timerfd_create.2.html),
[umask(2)](https://man7.org/man2/umask.2.html),
[vfork(2)](https://man7.org/man2/vfork.2.html),
[cap_get_file(3)](https://man7.org/man3/cap_get_file.3.html),
[cap_iab(3)](https://man7.org/man3/cap_iab.3.html),
[cap_launch(3)](https://man7.org/man3/cap_launch.3.html),
[catopen(3)](https://man7.org/man3/catopen.3.html),
[exec(3)](https://man7.org/man3/exec.3.html),
[exit(3)](https://man7.org/man3/exit.3.html),
[fexecve(3)](https://man7.org/man3/fexecve.3.html),
[getauxval(3)](https://man7.org/man3/getauxval.3.html),
[getexeccon(3)](https://man7.org/man3/getexeccon.3.html),
[getfscreatecon(3)](https://man7.org/man3/getfscreatecon.3.html),
[getkeycreatecon(3)](https://man7.org/man3/getkeycreatecon.3.html),
[getsockcreatecon(3)](https://man7.org/man3/getsockcreatecon.3.html),
[libexpect(3)](https://man7.org/man3/libexpect.3.html),
[mq_close(3)](https://man7.org/man3/mq_close.3.html),
[posix_spawn(3)](https://man7.org/man3/posix_spawn.3.html),
[pthread_atfork(3)](https://man7.org/man3/pthread_atfork.3.html),
[pthread_kill_other_threads_np(3)](https://man7.org/man3/pthread_kill_other_threads_np.3.html),
[pthread_mutexattr_setrobust(3)](https://man7.org/man3/pthread_mutexattr_setrobust.3.html),
[sd_bus_creds_get_pid(3)](https://man7.org/man3/sd_bus_creds_get_pid.3.html),
[sem_close(3)](https://man7.org/man3/sem_close.3.html),
[sigvec(3)](https://man7.org/man3/sigvec.3.html),
[system(3)](https://man7.org/man3/system.3.html),
[auditd-plugins(5)](https://man7.org/man5/auditd-plugins.5.html),
[core(5)](https://man7.org/man5/core.5.html),
[elf(5)](https://man7.org/man5/elf.5.html),
[proc_pid_attr(5)](https://man7.org/man5/proc_pid_attr.5.html),
[proc_pid_cmdline(5)](https://man7.org/man5/proc_pid_cmdline.5.html),
[proc_pid_environ(5)](https://man7.org/man5/proc_pid_environ.5.html),
[proc_sys_kernel(5)](https://man7.org/man5/proc_sys_kernel.5.html),
[systemd.exec(5)](https://man7.org/man5/systemd.exec.5.html),
[systemd-system.conf(5)](https://man7.org/man5/systemd-system.conf.5.html),
[capabilities(7)](https://man7.org/man7/capabilities.7.html),
[cgroups(7)](https://man7.org/man7/cgroups.7.html),
[credentials(7)](https://man7.org/man7/credentials.7.html),
[environ(7)](https://man7.org/man7/environ.7.html),
[inode(7)](https://man7.org/man7/inode.7.html),
[inotify(7)](https://man7.org/man7/inotify.7.html),
[persistent-keyring(7)](https://man7.org/man7/persistent-keyring.7.html),
[process-keyring(7)](https://man7.org/man7/process-keyring.7.html),
[pthreads(7)](https://man7.org/man7/pthreads.7.html),
[sched(7)](https://man7.org/man7/sched.7.html),
[session-keyring(7)](https://man7.org/man7/session-keyring.7.html),
[signal(7)](https://man7.org/man7/signal.7.html),
[signal-safety(7)](https://man7.org/man7/signal-safety.7.html),
[thread-keyring(7)](https://man7.org/man7/thread-keyring.7.html),
[user-keyring(7)](https://man7.org/man7/user-keyring.7.html),
[user_namespaces(7)](https://man7.org/man7/user_namespaces.7.html),
[user-session-keyring(7)](https://man7.org/man7/user-session-keyring.7.html),
[vdso(7)](https://man7.org/man7/vdso.7.html),
[pam_selinux(8)](https://man7.org/man8/pam_selinux.8.html)
