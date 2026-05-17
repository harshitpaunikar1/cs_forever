Title: FFmpeg: Main Page
Mapped Topic: Transcoding and streaming toolkit
Source URL: https://ffmpeg.org/doxygen/2.3/index.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:09:56+00:00
Mapped From CSE.md Section: Part 2: F. Audio / video / media systems

# Content

|
FFmpeg
|

FFmpeg Documentation

This document describes the usage of the different libraries provided by FFmpeg.

[libavcodec](https://ffmpeg.org/group__libavc.html)encoding/decoding library[libavfilter](https://ffmpeg.org/group__lavfi.html)graph-based frame editing library[libavformat](https://ffmpeg.org/group__libavf.html)I/O and muxing/demuxing library[libavdevice](https://ffmpeg.org/group__lavd.html)special devices muxing/demuxing library[libavutil](https://ffmpeg.org/group__lavu.html)common utility library[libswresample](https://ffmpeg.org/group__lswr.html)audio resampling, format conversion and mixing[libpostproc](https://ffmpeg.org/group__lpp.html)post processing library[libswscale](https://ffmpeg.org/group__libsws.html)color conversion and scaling library

*LIBRARYNAME_VERSION_{MAJOR,MINOR,MICRO}* macros. The major version number is incremented with backward incompatible changes - e.g. removing parts of the public API, reordering public struct members, etc. The minor version number is incremented for backward compatible API changes or major new features - e.g. adding a new public function or a new decoder. The micro version number is incremented for smaller changes that a calling program might still want to check for - e.g. changing behavior in a previously unspecified situation.

Generated on Sun Jul 20 2014 23:06:37 for FFmpeg by
