Title: FFmpeg: Main Page
Mapped Topic: Transcoding and streaming toolkit
Source URL: https://ffmpeg.org/doxygen/2.0/index.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:09:54+00:00
Mapped From CSE.md Section: Part 2: F. Audio / video / media systems

# Content

|
FFmpeg
|

FFmpeg Documentation

This document describes the usage of the different libraries provided by FFmpeg.

[libavcodec](https://ffmpeg.org/group__libavc.html)encoding/decoding library[libavfilter](https://ffmpeg.org/group__lavfi.html)graph-based frame editing library[libavformat](https://ffmpeg.org/group__libavf.html)I/O and muxing/demuxing library[libavdevice](https://ffmpeg.org/group__lavd.html)special devices muxing/demuxing library[libavutil](https://ffmpeg.org/group__lavu.html)common utility library[libswresample](https://ffmpeg.org/group__lswr.html)audio resampling, format conversion and mixing[libpostproc](https://ffmpeg.org/group__lpp.html)post processing library[libswscale](https://ffmpeg.org/group__lsws.html)color conversion and scaling library

Each of the FFmpeg libraries contains a version.h header, which defines a major, minor and micro version number with the *LIBRARYNAME_VERSION_{MAJOR,MINOR,MICRO}* macros. The major version number is incremented with backward incompatible changes - e.g. removing parts of the public API, reordering public struct members, etc. The minor version number is incremented for backward compatible API changes or major new features - e.g. adding a new public function or a new decoder. The micro version number is incremented for smaller changes that a calling program might still want to check for - e.g. changing behavior in a previously unspecified situation.

FFmpeg guarantees backward API and ABI compatibility for each library as long as its major version number is unchanged. This means that no public symbols will be removed or renamed. Types and names of the public struct members and values of public macros and enums will remain the same (unless they were explicitly declared as not part of the public API). Documented behavior will not change.

In other words, any correct program that works with a given FFmpeg snapshot should work just as well without any changes with any later snapshot with the same major versions. This applies to both rebuilding the program against new FFmpeg versions or to replacing the dynamic FFmpeg libraries that a program links against.

However, new public symbols may be added and new members may be appended to public structs whose size is not part of public ABI (most public structs in FFmpeg). New macros and enum values may be added. Behavior in undocumented situations may change slightly (and be documented). All those are accompanied by an entry in doc/APIchanges and incrementing either the minor or micro version number.

Generated on Wed Jul 10 2013 23:48:41 for FFmpeg by
