Title: D - Useful Development Tools - The Rust Programming Language
Mapped Topic: Rust book
Source URL: https://doc.rust-lang.org/book/appendix-04-useful-development-tools.html
Source Type: official_book
Trust Score: 97
Fetched At: 2026-04-17T07:07:36+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

[Appendix D: Useful Development Tools](https://doc.rust-lang.org#appendix-d-useful-development-tools)

In this appendix, we talk about some useful development tools that the Rust project provides. Weâll look at automatic formatting, quick ways to apply warning fixes, a linter, and integrating with IDEs.

[Automatic Formatting with ](https://doc.rust-lang.org#automatic-formatting-with-rustfmt)`rustfmt`

`rustfmt`

The `rustfmt`

tool reformats your code according to the community code style.
Many collaborative projects use `rustfmt`

to prevent arguments about which
style to use when writing Rust: Everyone formats their code using the tool.

Rust installations include `rustfmt`

by default, so you should already have the
programs `rustfmt`

and `cargo-fmt`

on your system. These two commands are
analogous to `rustc`

and `cargo`

in that `rustfmt`

allows finer grained control
and `cargo-fmt`

understands conventions of a project that uses Cargo. To format
any Cargo project, enter the following:

```
$ cargo fmt
```

Running this command reformats all the Rust code in the current crate. This
should only change the code style, not the code semantics. For more information
on `rustfmt`

, see [its documentation](https://github.com/rust-lang/rustfmt).

[Fix Your Code with ](https://doc.rust-lang.org#fix-your-code-with-rustfix)`rustfix`

`rustfix`

The `rustfix`

tool is included with Rust installations and can automatically
fix compiler warnings that have a clear way to correct the problem thatâs
likely what you want. Youâve probably seen compiler warnings before. For
example, consider this code:

Filename: src/main.rs

```
fn main() {
let mut x = 42;
println!("{x}");
}
```

Here, weâre defining the variable `x`

as mutable, but we never actually mutate
it. Rust warns us about that:

```
$ cargo build
Compiling myprogram v0.1.0 (file:///projects/myprogram)
warning: variable does not need to be mutable
--> src/main.rs:2:9
|
2 | let mut x = 0;
| ----^
| |
| help: remove this `mut`
|
= note: `#[warn(unused_mut)]` on by default
```

The warning suggests that we remove the `mut`

keyword. We can automatically
apply that suggestion using the `rustfix`

tool by running the command `cargo fix`

:

```
$ cargo fix
Checking myprogram v0.1.0 (file:///projects/myprogram)
Fixing src/main.rs (1 fix)
Finished dev [unoptimized + debuginfo] target(s) in 0.59s
```

When we look at *src/main.rs* again, weâll see that `cargo fix`

has changed the
code:

Filename: src/main.rs

```
fn main() {
let x = 42;
println!("{x}");
}
```

The variable `x`

is now immutable, and the warning no longer appears.

You can also use the `cargo fix`

command to transition your code between
different Rust editions. Editions are covered in [Appendix E](https://doc.rust-lang.org/appendix-05-editions.html).

[More Lints with Clippy](https://doc.rust-lang.org#more-lints-with-clippy)

The Clippy tool is a collection of lints to analyze your code so that you can catch common mistakes and improve your Rust code. Clippy is included with standard Rust installations.

To run Clippyâs lints on any Cargo project, enter the following:

```
$ cargo clippy
```

For example, say you write a program that uses an approximation of a mathematical constant, such as pi, as this program does:

Running `cargo clippy`

on this project results in this error:

```
error: approximate value of `f{32, 64}::consts::PI` found
--> src/main.rs:2:13
|
2 | let x = 3.1415;
| ^^^^^^
|
= note: `#[deny(clippy::approx_constant)]` on by default
= help: consider using the constant directly
= help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#approx_constant
```

This error lets you know that Rust already has a more precise `PI`

constant
defined, and that your program would be more correct if you used the constant
instead. You would then change your code to use the `PI`

constant.

The following code doesnât result in any errors or warnings from Clippy:

For more information on Clippy, see [its documentation](https://github.com/rust-lang/rust-clippy).

[IDE Integration Using ](https://doc.rust-lang.org#ide-integration-using-rust-analyzer)`rust-analyzer`

`rust-analyzer`

To help with IDE integration, the Rust community recommends using
[ rust-analyzer](https://rust-analyzer.github.io). This tool is a set of
compiler-centric utilities that speak

[Language Server Protocol](http://langserver.org/), which is a specification for IDEs and programming languages to communicate with each other. Different clients can use

`rust-analyzer`

, such as
[the Rust analyzer plug-in for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer).

Visit the `rust-analyzer`

projectâs [home page](https://rust-analyzer.github.io)
for installation instructions, then install the language server support in your
particular IDE. Your IDE will gain capabilities such as autocompletion, jump to
definition, and inline errors.
