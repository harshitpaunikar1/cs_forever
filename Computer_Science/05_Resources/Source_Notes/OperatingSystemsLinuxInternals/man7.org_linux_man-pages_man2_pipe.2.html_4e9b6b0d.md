Title: pipe(2) - Linux manual page
Mapped Topic: Linux systems programming interfaces
Source URL: https://man7.org/linux/man-pages/man2/pipe.2.html
Source Type: official_reference
Trust Score: 96
Fetched At: 2026-04-17T07:05:32+00:00
Mapped From CSE.md Section: Part 2: C. Operating systems, Linux internals, kernel understanding

# Content

|
|
|
|
|

```
```*pipe*(2) System Calls Manual *pipe*(2)

pipe, pipe2 - create pipe

Standard C library (libc,-lc)

#include <unistd.h>int pipe(intpipefd[2]);#define _GNU_SOURCE/* See feature_test_macros(7) */#include <fcntl.h>/* Definition ofO_*constants */#include <unistd.h>int pipe2(intpipefd[2], intflags);/* On Alpha, IA-64, MIPS, SuperH, and SPARC/SPARC64, pipe() has the following prototype; see VERSIONS */#include <unistd.h>struct fd_pair {long fd[2];};struct fd_pair pipe(void);

pipe() creates a pipe, a unidirectional data channel that can be used for interprocess communication. The arraypipefdis used to return two file descriptors referring to the ends of the pipe.pipefd[0]refers to the read end of the pipe.pipefd[1]refers to the write end of the pipe. Data written to the write end of the pipe is buffered by the kernel until it is read from the read end of the pipe. For further details, see[pipe(7)]. Ifflagsis 0, thenpipe2() is the same aspipe(). The following values can be bitwise ORed inflagsto obtain different behavior:O_CLOEXECSet the close-on-exec (FD_CLOEXEC) flag on the two new file descriptors. See the description of the same flag in[open(2)]for reasons why this may be useful.O_DIRECT(since Linux 3.4) Create a pipe that performs I/O in "packet" mode. Each[write(2)]to the pipe is dealt with as a separate packet, and[read(2)]s from the pipe will read one packet at a time. Note the following points: â¢ Writes of greater thanPIPE_BUFbytes (see[pipe(7)]) will be split into multiple packets. The constantPIPE_BUFis defined in<limits.h>. â¢ If a[read(2)]specifies a buffer size that is smaller than the next packet, then the requested number of bytes are read, and the excess bytes in the packet are discarded. Specifying a buffer size ofPIPE_BUFwill be sufficient to read the largest possible packets (see the previous point). â¢ Zero-length packets are not supported. (A[read(2)]that specifies a buffer size of zero is a no-op, and returns 0.) Older kernels that do not support this flag will indicate this via anEINVALerror. Since Linux 4.5, it is possible to change theO_DIRECTsetting of a pipe file descriptor using[fcntl(2)].O_NONBLOCKSet theO_NONBLOCKfile status flag on the open file descriptions referred to by the new file descriptors. Using this flag saves extra calls to[fcntl(2)]to achieve the same result.O_NOTIFICATION_PIPESince Linux 5.8, general notification mechanism is built on the top of the pipe where kernel splices notification messages into pipes opened by user space. The owner of the pipe has to tell the kernel which sources of events to watch and filters can also be applied to select which subevents should be placed into the pipe.

On success, zero is returned. On error, -1 is returned,is set to indicate the error, and[errno]pipefdis left unchanged. On Linux (and other systems),pipe() does not modifypipefdon failure. A requirement standardizing this behavior was added in POSIX.1-2008 TC2. The Linux-specificpipe2() system call likewise does not modifypipefdon failure.

EFAULTpipefdis not valid.EINVAL(pipe2()) Invalid value inflags.EMFILEThe per-process limit on the number of open file descriptors has been reached.ENFILEThe system-wide limit on the total number of open files has been reached.ENFILEThe user hard limit on memory that can be allocated for pipes has been reached and the caller is not privileged; see[pipe(7)].ENOPKG(pipe2())O_NOTIFICATION_PIPEwas passed inflagsand support for notifications (CONFIG_WATCH_QUEUE) is not compiled into the kernel.

The System V ABI on some architectures allows the use of more than one register for returning multiple values; several architectures (namely, Alpha, IA-64, MIPS, SuperH, and SPARC/SPARC64) (ab)use this feature in order to implement thepipe() system call in a functional manner: the call doesn't take any arguments and returns a pair of file descriptors as the return value on success. The glibcpipe() wrapper function transparently deals with this. See[syscall(2)]for information regarding registers used for storing second file descriptor.

POSIX.1-2024.

pipe() POSIX.1-2001.pipe2() POSIX.1-2024. Linux 2.6.27, glibc 2.9.

The following program creates a pipe, and then[fork(2)]s to create a child process; the child inherits a duplicate set of file descriptors that refer to the same pipe. After the[fork(2)], each process closes the file descriptors that it doesn't need for the pipe (see[pipe(7)]). The parent then writes the string contained in the program's command-line argument to the pipe, and the child reads this string a byte at a time from the pipe and echoes it on standard output.Program source#include <err.h> #include <stdio.h> #include <stdlib.h> #include <string.h> #include <sys/types.h> #include <sys/wait.h> #include <unistd.h> int main(int argc, char *argv[]) { int pipefd[2]; char buf; pid_t cpid; if (argc != 2) { fprintf(stderr, "Usage: %s <string>\n", argv[0]); exit(EXIT_FAILURE); } if (pipe(pipefd) == -1) err(EXIT_FAILURE, "pipe"); cpid = fork(); if (cpid == -1) err(EXIT_FAILURE, "fork"); if (cpid == 0) { /* Child reads from pipe */ if (close(pipefd[1]) == -1) /* Close unused write end */ err(EXIT_FAILURE, "close"); while (read(pipefd[0], &buf, 1) > 0) { if (write(STDOUT_FILENO, &buf, 1) != 1) err(EXIT_FAILURE, "write"); } if (write(STDOUT_FILENO, "\n", 1) != 1) err(EXIT_FAILURE, "write"); if (close(pipefd[0]) == -1) err(EXIT_FAILURE, "close"); _exit(EXIT_SUCCESS); } else { /* Parent writes argv[1] to pipe */ if (close(pipefd[0]) == -1) /* Close unused read end */ err(EXIT_FAILURE, "close"); if (write(pipefd[1], argv[1], strlen(argv[1])) != strlen(argv[1])) err(EXIT_FAILURE, "write"); if (close(pipefd[1]) == -1) /* Reader will see EOF */ err(EXIT_FAILURE, "close"); if (wait(NULL) == -1) /* Wait for child */ err(EXIT_FAILURE, "wait"); exit(EXIT_SUCCESS); } }

[fork(2)],[read(2)],[socketpair(2)],[splice(2)],[tee(2)],[vmsplice(2)],[write(2)],[popen(3)],[pipe(7)]

This page is part of theman-pages(Linux kernel and C library user-space interface documentation) project. Information about the project can be found at â¨[https://www.kernel.org/doc/man-pages/]â©. If you have a bug report for this manual page, see â¨[https://git.kernel.org/pub/scm/docs/man-pages/man-pages.git/tree/CONTRIBUTING]â©. This page was obtained from the tarball man-pages-6.16.tar.gz fetched from â¨[https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/]â© on 2026-01-16. If you discover any rendering problems in this HTML version of the page, or you believe there is a better or more up- to-date source for the page, or you have corrections or improvements to the information in this COLOPHON (which isnotpart of the original manual page), send a mail to man-pages@man7.org Linux man-pages 6.16 2025-10-29pipe(2)

Pages that refer to this page:
[eventfd(2)](https://man7.org/man2/eventfd.2.html),
[fork(2)](https://man7.org/man2/fork.2.html),
[getrlimit(2)](https://man7.org/man2/getrlimit.2.html),
[ioctl_pipe(2)](https://man7.org/man2/ioctl_pipe.2.html),
[socketpair(2)](https://man7.org/man2/socketpair.2.html),
[statfs(2)](https://man7.org/man2/statfs.2.html),
[syscall(2)](https://man7.org/man2/syscall.2.html),
[syscalls(2)](https://man7.org/man2/syscalls.2.html),
[io_uring_prep_pipe(3)](https://man7.org/man3/io_uring_prep_pipe.3.html),
[pmda(3)](https://man7.org/man3/pmda.3.html),
[pmdaconnect(3)](https://man7.org/man3/pmdaconnect.3.html),
[__pmprocesspipe(3)](https://man7.org/man3/__pmprocesspipe.3.html),
[popen(3)](https://man7.org/man3/popen.3.html),
[capabilities(7)](https://man7.org/man7/capabilities.7.html),
[fifo(7)](https://man7.org/man7/fifo.7.html),
[inode(7)](https://man7.org/man7/inode.7.html),
[man-pages(7)](https://man7.org/man7/man-pages.7.html),
[pipe(7)](https://man7.org/man7/pipe.7.html),
[signal-safety(7)](https://man7.org/man7/signal-safety.7.html)
