Title: Modern C
Mapped Topic: C23-oriented C foundations
Source URL: https://gustedt.gitlabpages.inria.fr/modern-c/
Source Type: official_open_book
Trust Score: 93
Fetched At: 2026-04-17T07:06:29+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Modern C

## Table of Contents

[Jens Gustedt](http://icube-icps.unistra.fr/index.php/Jens\_Gustedt)

[(@JensGustedt@digitalcourage.social)](https://digitalcourage.social/@JensGustedt)

## 1. The C23 edition of Modern C

The free version of this edition is available at

This new edition has been the occasion to overhaul the presentation in
many places, but its main purpose is the update to the new C standard,
[C23](https://www.iso.org/standard/82075.html). The goal was to publish this new edition of Modern C at the same
time as the new C standard goes through the procedure of ISO
publication. The closest approximation of the contents of the new
standard in a publically available document can be found [here](https://www.open-std.org/JTC1/SC22/WG14/www/docs/n3220.pdf). New
releases of major compilers already implement most of the new features
that it brings.

Among the most noticeable changes and additions that we handle are
those for integers: there are new bit-precise types coined
`_BitInt(N)`

, new C library headers `<stdckdint.h>`

(for arithmetic
with overflow check) and `<stdbit.h>`

(for bit manipulation),
possibilities for 128 bit types on modern architectures, and
substantial improvements for enumeration types. Other new concepts in
C23 include a `nullptr`

constant and its underlying type, syntactic
annotation with attributes, more tools for type generic programming
such as type inference with `auto`

and `typeof`

, default
initialization with `{}`

, even for variable length arrays, and
`constexpr`

for name constants of any type. Furthermore, new material
has been added, discussing compound expressions and lambdas, so-called
“internationalization”, a comprehensive approach for program failure.

Also added has been an appendix and a temporary include header for an easy transition to C23 on existing platforms, that will allow you to start off with C23 right away.

## 2. Online resources

### 2.1. Downloads

The most recent version available is from Oct. 15, 2024.

- a CC licensed version of
*Modern C* - a MIT licensed version of the code examples
- is
*archived here* - may be downloaded as
[zip file](https://gustedt.gitlabpages.inria.fr/modernC-code.zip).

- is

### 2.2. [Blog](https://gustedt.wordpress.com/)

I sometimes use my blog to dump new ideas where I think C should head to, and to keep an updated list of the features that might go into C2x.

## 3. Print version

Print and eBook editions of Modern C by Manning for the C23 version are available since Sep. 1, 2025

They have the same contents as the public version above, but there may be some notable differences in numbering and layout.

There is a special code **au35gus** to get 35% off of the official
price from all Manning products, including Modern C.

## 4. Be a sponsor

I am not producing this book for a living. If you think that you don't want to buy a printed or e-paper version and are satisfied by using the public version, you're welcome to do so.

You could still think of contributing a little bit, either by volunteering to

- your favorite software project
- a software industry improvement project
- a free speech or publication project
- the national C standards committee of your country

or anything else that makes the whole world (or maybe just our planet) a better place.

You could also contribute by giving whatever money you may spare to such a project. There are many projects in need of contributions, not all important open source projects out there are financed by big money, and that independence is important.

## 5. Terms

### 5.1. Licence for this version of the book itself

### 5.2. Copyright and License of provided source code

The C source code provided with this book is licensed under the following standard MIT license: ---------------------------------------------------------------------- Copyright © 2015-2024 Jens Gustedt Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. ----------------------------------------------------------------------
