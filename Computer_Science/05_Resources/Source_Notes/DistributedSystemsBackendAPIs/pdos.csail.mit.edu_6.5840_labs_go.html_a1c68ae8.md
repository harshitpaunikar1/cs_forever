Title: 6.5840 Go
Mapped Topic: Distributed systems labs and schedule
Source URL: https://pdos.csail.mit.edu/6.5840/labs/go.html
Source Type: official_course
Trust Score: 97
Fetched At: 2026-04-17T07:00:43+00:00
Mapped From CSE.md Section: Part 1 / Part 2.E

# Content

### Go

You'll implement all the labs in
[Go](http://www.golang.org/). The Go web site contains lots
of tutorial information. You should use Go 1.22 or any later version.
You can check your Go version by running `go version`.

We recommend that you work on the labs on your own machine, so you can
use the tools, text editors, etc. that you are already familiar with. Many
editors have plug-ins for Go, e.g.
the
[Go extension](https://code.visualstudio.com/docs/languages/go) for
VS Code. Some commercial IDEs like
[GoLand](https://www.jetbrains.com/go/) have
[free educational licenses](https://www.jetbrains.com/community/education/#students).
We are happy to provide support over Piazza and in office hours to help
you set up Go.
The labs probably won't work on Athena.

#### macOS

You can use [Homebrew](https://brew.sh/) to install Go. After
installing Homebrew, run `brew install go`.

#### Linux

Depending on your Linux distribution, you might be able to get an up-to-date
version of Go from the package repository, e.g. by running `apt install
golang`. Otherwise, you can manually install a binary from Go's website.
First, make sure that you're running a 64-bit kernel (`uname -a` should
mention "x86_64 GNU/Linux"), and then run:

$ wget -qO- https://go.dev/dl/go1.23.5.linux-amd64.tar.gz | sudo tar xz -C /usr/local

You'll need to make sure `/usr/local/go/bin` is on your `PATH`.
You can do this by adding `export PATH=$PATH:/usr/local/go/bin` to your
shell's init file ( commonly this is one of `.bashrc`, `.bash_profile` or `.zshrc`)
#### Windows

The labs are believed to work under Microsoft's WSL2 (Windows Subsystem for
Linux, version 2).

To use WSL 2, first make sure you have
the [Windows
Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) installed. Then
add [Ubuntu
24.04 from the Microsoft Store](https://apps.microsoft.com/detail/9nz3klhxdjp5). Afterwards you should be able to
launch Ubuntu Linux. Then you can follow
the directions for Linux (above).

Make sure that you are running version 2 of WSL.
WSL 1 does not work with the labs.
To check,
run ` wsl -l -v `

in a Windows terminal to confirm that WSL
2 and the correct Ubuntu version are installed.
