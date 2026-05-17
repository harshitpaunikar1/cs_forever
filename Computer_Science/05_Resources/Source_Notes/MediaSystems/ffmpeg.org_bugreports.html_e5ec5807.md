Title: Bug Reports
Mapped Topic: Transcoding and streaming toolkit
Source URL: https://ffmpeg.org/bugreports.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:09:43+00:00
Mapped From CSE.md Section: Part 2: F. Audio / video / media systems

# Content

Before reporting a bug, please consider the following:

FFmpeg is in a state of perpetual development.

As such, if you wish to query or report a bug, you must try with the **latest development branch** revision of FFmpeg to confirm the issue still exists.

When writing your bug report, please include (uncompressed):

- What you were trying to accomplish (e.g., "I am trying to transcode
from this format to that format...")
- The problem you encountered (e.g., "ffmpeg crashed, see the
gdb and valgrind output below" or "The
output video was all green")
- The exact command line you were using (e.g., "
```
ffmpeg -i input.mov
-an -vcodec foo output.avi
```

")
- The full, uncut console output provided by
`ffmpeg -v 9 -loglevel 99 -i `

followed by the name of your input file
(copy/pasted from the console, including the banner that indicates
version and configuration options), paste ffplay or ffprobe output
only if your problem is not reproducible with ffmpeg.
- Sufficient information, including any required input files, to reproduce
the bug and confirm a potential fix.

You can use the `-report`

option or define the
`FFREPORT`

environment variable (to any value) to get the exact
command line and the full verbose console output in a file named
`ffmpeg-*.log`

in the current directory.

If you encounter a crash bug, please provide the

`gdb`

output,
backtrace and disassembly, and if possible the

`valgrind`

output,
using the the

`ffmpeg_g`

debug binary.

For `gdb`

, proceed as follows:

gdb ffmpeg_g

In `gdb`

, type 'r' for run, along with the rest of the
`ffmpeg`

command line:

r <rest of command line>

*
Alternatively, you can run *```
gdb --args ffmpeg_g <rest of command
line>
```

and just type 'r' at the `gdb`

prompt.
When `gdb`

encounters its problem, run the following commands and
copy/paste the output into your bug report:

bt
disass $pc-32,$pc+32
info all-registers

With older `gdb`

versions, use `disass $pc-32 $pc+32`

.

For `valgrind`

, run the following command and copy/paste the
output into your bug report:

valgrind ffmpeg_g <rest of command line>

If you encounter a regression, please use `git bisect`

to find the
revission that caused the regression. Having this information available can
greatly speed up correcting the bug.

###
Bug Tracker

Once you have gathered this information, you can submit a report to the
[FFmpeg bug tracker](https://trac.ffmpeg.org).

*Note, you must *[register](https://trac.ffmpeg.org/register)
there first before you can submit a report.

You should provide all information so that anyone can reproduce the bug.

Please do not report your problem on the developer mailing list:

Only send bug reports there if you also intend to provide a fix.

The developers may ask you to provide a sample media file illustrating
your problem. In this case, please follow these steps:

- If the sample file is too large ( > 10 megabytes), cut it down to
size with the Unix 'dd' command:

dd if=sample-file of=small-sample-file bs=1024 count=10000

and then upload small-sample-file rather than sample-file

- Please choose descriptive names like
`h264_green_tint.mov`

or
`block_artifacts_after_seeking.mkv`

. We already have plenty of `bug.rm`

and `sample.avi`

.

- Upload the sample with the VideoLAN file uploader.

- Go to
[streams.videolan.org/upload/](https://streams.videolan.org/upload/)
- Select the FFmpeg Project.
- Fill in the FFmpeg version in the VLC version field.
- Put the corresponding Trac ticket number in the GitLab ticket field, if a ticket exists.
- Write a brief describing of the sample and what is wrong.
- Upload the sample. Note that the file size limit is 1024M, file exceeding that are discarded.

- Email the ffmpeg mailing list and indicate the filename of the sample.

Movie files which have been compressed (rar,7z,gzip,...) will be
deleted without being examined unless they are raw RGB/YUV/PCM.

Furthermore movie files uploaded to services like rapidshare or
any other similar service will be ignored. We are not willing to spend our
time fighting with this ridiculous, bloated and spam-filled crap.

Hosting provided by [telepoint.bg](https://telepoint.bg)
