Title: Download FFmpeg
Mapped Topic: Transcoding and streaming toolkit
Source URL: https://ffmpeg.org/download.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:09:47+00:00
Mapped From CSE.md Section: Part 2: F. Audio / video / media systems

# Content

####
If you find FFmpeg useful, you are welcome to contribute
by [donating](https://ffmpeg.org/donations.html).
More downloading options

### Get packages & executable files

FFmpeg only provides source code. Below are some links that provide it already compiled and ready to go.

### Linux Packages

**Debian**â Official packages for Stable-Backports, Testing, Unstable

**Debian**â deb-multimedia packages for Oldstable, Stable, Testing, Unstable

**Ubuntu**â Official packages

**Fedora**and**Red Hat Enterprise Linux**packages### Linux Static Builds

### Windows EXE Files

### Get the Sources

You can retrieve the source code through
[Git](https://git-scm.com/)
by using the command:

git clone https://git.ffmpeg.org/ffmpeg.git ffmpeg

FFmpeg has always been a very experimental and developer-driven project. It is a key component in many multimedia projects and has new features added constantly. Development branch snapshots work really well 99% of the time so people are not afraid to use them.

#### Git Repositories

Since FFmpeg is developed with [Git](https://git-scm.com/),
multiple repositories from developers and groups of developers are available.

| Clone URL | Description |
|---|---|
| Main FFmpeg Git repository | |
|

[https://git.ffmpeg.org/fateserver](https://git.ffmpeg.org/fateserver)[fate.ffmpeg.org](http://fate.ffmpeg.org)server software repository#### Release Verification

All FFmpeg releases are cryptographically signed with
[our public PGP key](https://ffmpeg.org/ffmpeg-devel.asc) and should be verified for
authenticity.

pub rsa2048 2011-04-26 [SC] FCF986EA15E6E293A5644F10B4322F04D67658D8 uid [ full ] FFmpeg release signing key <ffmpeg-devel@ffmpeg.org> sub rsa2048 2011-04-26 [E]

To verify a release:

- Import our public key into your local keyring:
$ curl https://ffmpeg.org/ffmpeg-devel.asc | gpg --import

- Download a release tarball and its corresponding signature.
-
Verify the signature:
$ gpg --verify ffmpeg-4.3.2.tar.xz.asc ffmpeg-4.3.2.tar.xz gpg: Signature made Sun 21 Feb 2021 06:35:15 AEST gpg: using RSA key FCF986EA15E6E293A5644F10B4322F04D67658D8 gpg: issuer "ffmpeg-devel@ffmpeg.org" gpg: Good signature from "FFmpeg release signing key <ffmpeg-devel@ffmpeg.org>" [full]

[EDDSA key DD1EC9E8DE085C629B3E1846B18E8928B3948D64](https://ffmpeg.org/git-tag-key.asc)

#### Releases

Approximately every 6 months the FFmpeg project makes a new major release. Between major releases point releases will appear that add important bug fixes but no new features. Note that these releases are intended for distributors and system integrators. Users that wish to compile from source themselves are strongly encouraged to consider using the development branch (see above), this is the only version on which FFmpeg developers actively work. The release branches only cherry pick selected changes from the development branch, which therefore receives much more and much faster bug fixes such as additional features and security patches.

### FFmpeg 8.1 "Hoare"

8.1 was released on 2026-03-16. It is the latest stable FFmpeg release from the 8.1 release branch, which was cut from master on 2026-03-08.

It includes the following library versions:

libavutil 60. 26.100 libavcodec 62. 28.100 libavformat 62. 12.100 libavdevice 62. 3.100 libavfilter 11. 14.100 libswscale 9. 5.100 libswresample 6. 3.100

### FFmpeg 8.0.1 "Huffman"

8.0.1 was released on 2025-11-20. It is the latest stable FFmpeg release from the 8.0 release branch, which was cut from master on 2025-08-09.

It includes the following library versions:

libavutil 60. 8.100 libavcodec 62. 11.100 libavformat 62. 3.100 libavdevice 62. 1.100 libavfilter 11. 4.100 libswscale 9. 1.100 libswresample 6. 1.100

### FFmpeg 7.1.3 "PÃ©ter"

7.1.3 was released on 2025-11-21. It is the latest stable FFmpeg release from the 7.1 release branch, which was cut from master on 2024-09-24.

It includes the following library versions:

libavutil 59. 39.100 libavcodec 61. 19.100 libavformat 61. 7.100 libavdevice 61. 3.100 libavfilter 10. 4.100 libswscale 8. 3.100 libswresample 5. 3.100 libpostproc 58. 3.100

### FFmpeg 7.0.3 "Dijkstra"

7.0.3 was released on 2025-08-05. It is the latest stable FFmpeg release from the 7.0 release branch, which was cut from master on 2024-03-27.

It includes the following library versions:

libavutil 59. 8.100 libavcodec 61. 3.100 libavformat 61. 1.100 libavdevice 61. 1.100 libavfilter 10. 1.100 libswscale 8. 1.100 libswresample 5. 1.100 libpostproc 58. 1.100

### FFmpeg 6.1.4 "Heaviside"

6.1.4 was released on 2025-11-23. It is the latest stable FFmpeg release from the 6.1 release branch, which was cut from master on 2023-10-29.

It includes the following library versions:

libavutil 58. 29.100 libavcodec 60. 31.102 libavformat 60. 16.100 libavdevice 60. 3.100 libavfilter 9. 12.100 libswscale 7. 5.100 libswresample 4. 12.100 libpostproc 57. 3.100

### FFmpeg 5.1.8 "Riemann"

5.1.8 was released on 2025-11-26. It is the latest stable FFmpeg release from the 5.1 release branch, which was cut from master on 2022-07-13.

It includes the following library versions:

libavutil 57. 28.100 libavcodec 59. 37.100 libavformat 59. 27.100 libavdevice 59. 7.100 libavfilter 8. 44.100 libswscale 6. 7.100 libswresample 4. 7.100 libpostproc 56. 6.100

### FFmpeg 4.4.6 "Rao"

4.4.6 was released on 2025-05-17. It is the latest stable FFmpeg release from the 4.4 release branch, which was cut from master on 2021-04-08.

It includes the following library versions:

libavutil 56. 70.100 libavcodec 58.134.100 libavformat 58. 76.100 libavdevice 58. 13.100 libavfilter 7.110.100 libswscale 5. 9.100 libswresample 3. 9.100 libpostproc 55. 9.100

### FFmpeg 4.3.9 "4:3"

4.3.9 was released on 2025-03-12. It is the latest stable FFmpeg release from the 4.3 release branch, which was cut from master on 2020-06-08.

It includes the following library versions:

libavutil 56. 51.100 libavcodec 58. 91.100 libavformat 58. 45.100 libavdevice 58. 10.100 libavfilter 7. 85.100 libswscale 5. 7.100 libswresample 3. 7.100 libpostproc 55. 7.100

### FFmpeg 4.2.11 "Ada"

4.2.11 was released on 2025-05-17. It is the latest stable FFmpeg release from the 4.2 release branch, which was cut from master on 2019-07-21.

It includes the following library versions:

libavutil 56. 31.100 libavcodec 58. 54.100 libavformat 58. 29.100 libavdevice 58. 8.100 libavfilter 7. 57.100 libswscale 5. 5.100 libswresample 3. 5.100 libpostproc 55. 5.100

### FFmpeg 3.4.14 "Cantor"

3.4.14 was released on 2025-03-12. It is the latest stable FFmpeg release from the 3.4 release branch, which was cut from master on 2017-10-11.

It includes the following library versions:

libavutil 55. 78.100 libavcodec 57.107.100 libavformat 57. 83.100 libavdevice 57. 10.100 libavfilter 6.107.100 libavresample 3. 7. 0 libswscale 4. 8.100 libswresample 2. 9.100 libpostproc 54. 7.100

### FFmpeg 2.8.22 "Feynman"

2.8.22 was released on 2023-10-29. It is the latest stable FFmpeg release from the 2.8 release branch, which was cut from master on 2015-09-05. Amongst lots of other changes, it includes all changes from ffmpeg-mt, libav master of 2015-08-28, libav 11 as of 2015-08-28.

It includes the following library versions:

libavutil 54. 31.100 libavcodec 56. 60.100 libavformat 56. 40.101 libavdevice 56. 4.100 libavfilter 5. 40.101 libavresample 2. 1. 0 libswscale 3. 1.101 libswresample 1. 2.101 libpostproc 53. 3.100

### Old Releases

Older versions are available at the [Old
Releases](https://ffmpeg.org/olddownload.html) page. Releases are usually moved there after the last
[downstream](https://trac.ffmpeg.org/wiki/Downstreams)
drops support.

Hosting provided by [telepoint.bg](https://telepoint.bg)
