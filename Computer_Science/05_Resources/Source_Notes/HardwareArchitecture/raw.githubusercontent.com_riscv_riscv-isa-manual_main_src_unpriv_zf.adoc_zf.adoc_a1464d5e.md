Title: zf.adoc
Mapped Topic: Instruction set architecture depth
Source URL: https://raw.githubusercontent.com/riscv/riscv-isa-manual/main/src/unpriv/zf.adoc
Source Type: github_official_repo
Trust Score: 97
Fetched At: 2026-04-17T07:02:08+00:00
Mapped From CSE.md Section: Part 2: A. Hardware, CPU, GPU, architecture, chip basics

# Content

[[zf]]
== Scalar Floating-Point Extensions

NOTE: This chapter is currently being restructured.
Its contents are normative, but the presentation might appear disjoint.

This chapter describes the scalar floating-point extensions.
The <<single-float,`F`>> extension adds floating-point registers and
instructions for computation on single-precision floating-point values.
The <<chap:d,`D`>> and <<quad-float,`Q`>> extensions widen those registers to
hold double- and quad-precision floating-point values, respectively, and add
instructions for computation on those formats.
Several additional extensions with the `Zf` and `Zd` prefixes provide
additional computational instructions.

The <<sec:zfinx,`Zfinx`>> and <<sec:zdinx,`Zdinx`>> extensions add
computational instructions analogous to those in the `F` and `D` extensions,
but they instead operate on floating-point numbers in the `x` registers.
These extensions, intended for lower-cost systems, are incompatible with the
`F` and `D` extensions.

include::f-st-ext.adoc[]
include::d-st-ext.adoc[]
include::q-st-ext.adoc[]
include::zfh.adoc[]
include::zfhmin.adoc[]
include::zfa.adoc[]
include::zfbfmin.adoc[]
include::zfinx.adoc[]
