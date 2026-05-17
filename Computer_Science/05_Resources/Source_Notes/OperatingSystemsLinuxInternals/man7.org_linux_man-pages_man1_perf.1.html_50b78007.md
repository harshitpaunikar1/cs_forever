Title: perf(1) - Linux manual page
Mapped Topic: Linux systems programming interfaces
Source URL: https://man7.org/linux/man-pages/man1/perf.1.html
Source Type: official_reference
Trust Score: 96
Fetched At: 2026-04-17T07:05:33+00:00
Mapped From CSE.md Section: Part 2: C. Operating systems, Linux internals, kernel understanding

# Content

|
|
|
|
|

```
```*PERF*(1) perf Manual *PERF*(1)

perf - Performance analysis tools for Linux

perf[--version] [--help] [OPTIONS] COMMAND [ARGS]

-h, --help Run perf help command. -v, --version Display perf version. -vv Print the compiled-in status of libraries. --exec-path Display or set exec path. --html-path Display html documentation path. -p, --paginate Set up pager. --no-pager Do not set pager. --buildid-dir Setup buildid cache directory. It has higher priority than buildid.dir config file option. --list-cmds List the most commonly used perf commands. --list-opts List available perf options. --debugfs-dir Set debugfs directory or set environment variable PERF_DEBUGFS_DIR. --debug Setup debug variable (see list below) in value range (0, 10). Use like: --debug verbose # sets verbose = 1 --debug verbose=2 # sets verbose = 2 List of debug variables allowed to set: verbose - general debug messages ordered-events - ordered events object debug messages data-convert - data convert command debug messages stderr - write debug output (option -v) to stderr in browser mode perf-event-open - Print perf_event_open() arguments and return value kmaps - Print kernel and module maps (perf script and perf report without browser) --debug-file Write debug output to a specified file.

Performance counters for Linux are a new kernel-based subsystem that provide a framework for all things performance analysis. It covers hardware level (CPU/PMU, Performance Monitoring Unit) features and software features (software counters, tracepoints) as well.

[perf-stat(1)],[perf-top(1)],[perf-record(1)],[perf-report(1)],[perf-list(1)][perf-amd-ibs(1)],[perf-annotate(1)],[perf-archive(1)],[perf-arm-spe(1)],[perf-bench(1)],[perf-buildid-cache(1)],[perf-buildid-list(1)],[perf-c2c(1)],[perf-config(1)],[perf-data(1)],[perf-diff(1)],[perf-evlist(1)],[perf-ftrace(1)],[perf-help(1)],[perf-inject(1)],[perf-intel-pt(1)],[perf-iostat(1)],[perf-kallsyms(1)],[perf-kmem(1)],[perf-kvm(1)],[perf-lock(1)],[perf-mem(1)],[perf-probe(1)],[perf-sched(1)],[perf-script(1)],[perf-test(1)],[perf-trace(1)],[perf-version(1)]

This page is part of theperf(Performance analysis tools for Linux (in Linux source tree)) project. Information about the project can be found at â¨[https://perf.wiki.kernel.org/index.php/Main_Page]â©. If you have a bug report for this manual page, send it to linux-kernel@vger.kernel.org. This page was obtained from the project's upstream Git repository â¨[http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git]â© on 2026-01-16. (At that time, the date of the most recent commit that was found in the repository was 2026-01-15.) If you discover any rendering problems in this HTML version of the page, or you believe there is a better or more up-to-date source for the page, or you have corrections or improvements to the information in this COLOPHON (which isnotpart of the original manual page), send a mail to man-pages@man7.org perf 2024-06-20PERF(1)

Pages that refer to this page:
[perf-bench(1)](https://man7.org/man1/perf-bench.1.html),
[perf-config(1)](https://man7.org/man1/perf-config.1.html),
[perf-data(1)](https://man7.org/man1/perf-data.1.html),
[perf-help(1)](https://man7.org/man1/perf-help.1.html),
[perf-lock(1)](https://man7.org/man1/perf-lock.1.html),
[perf_event_open(2)](https://man7.org/man2/perf_event_open.2.html)
