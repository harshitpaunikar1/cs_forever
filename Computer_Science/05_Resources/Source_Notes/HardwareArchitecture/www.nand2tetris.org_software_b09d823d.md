Title: Software | nand2tetris
Mapped Topic: Hardware-software bridge
Source URL: https://www.nand2tetris.org/software
Source Type: official_course
Trust Score: 95
Fetched At: 2026-04-17T06:54:08+00:00
Mapped From CSE.md Section: Part 1 / Part 2.A

# Content

## Software

Nand to Tetris courses, and the book The Elements of Computing Systems, are accompanied by a set of software tools. These tools enable the completion and testing of all the projects described in the courses and in the book. The tools are available in one package that comes in two versions:

[Nand to Tetris Online IDE:](https://nand2tetris.github.io/web-ide/chip/) This new Integrated Development Environment is web-based, meaning that you don’t have to download anything: All the tools and files necessary for completing all the projects are available from your browser. The files that you’ll develop using this IDE will be saved automatically in your browser’s memory, and you’ll be able to download them to your local PC.

[Nand to Tetris Software package](https://drive.google.com/open?id=1IkIR8Pwq3PY49QgXpUJOkUUVht-TKIET&usp=drive_fs): In this legacy “desktop version”, the tools are implemented as Java programs that run on your local PC. In order to use this version of the tools, you must download a zip file to your PC, and extract it. Also, your PC should be able to run Java programs.

The recommended go-to option is the new IDE, which is easy to use and requires no installation. The desktop version is provided for backward compatibility reasons.

All the software tools, in both versions, are supplied freely, in open source.

The Nand2tetris Software Suite consists of two folders: projects, and tools.

The projects folder is divided into 14 project folders named 00, 01, ..., 13. These folders contain files that you have to modify and complete as you work on various nand2tetris projects.

The tools folder contains the nand2tetris software tools. It's a collection of programs and files that will be explained as you follow the various projects.

The remainder of this section should be used as reference; there is no need to read what follows until you will be asked to use a particular software tool.

The .bat and .sh files are batch and script files, used to invoke the nand2tetris software tools. These files are explained in detail below.

The bin folder contains the code of the nand2tetris software tools. It consists of several sub-folders containing Java class files and supporting files.

The builtInChips and the builtInVMCode folders contain files that are used by the supplied Hardware Simulator and VM Emulator, respectively.

The OS folder contains a compiled version of the Jack operating system.

Tool

Tool

Hardware Simulator

Description

Test Scripts

Test Scripts

Simulating a Xor gate

Running a test script

Simulating the topmost Computer chip

Tool

CPU Emulator

Test Scripts

Running a machine language program that draws a rectangle on the computer screen

Tool

VM Emulator

Test Scripts

Running a VM program

Tool

Assembler

Test Scripts

Using a

compare file

Tool

Compiler

Description

Translates programs written in Jack (a simple, Java-like object-based language) into VM code. The resulting code can run on the supplied VM Emulator. Alternatively, the VM code can be translated further by the supplied VM translatorinto Hack assembly code that can then be executed on the supplied CPU Emulator.

Test Scripts

(A GUI-less, command-level program)

Tool

Operating system

Description

Two OS implementations are supplied: (i) a collection of eight .vm class files, written originally in Jack (just like Unix is written in C), and (ii) a faster implementation of all the OS services, embedded in the supplied VM Emulator.

Test Scripts

(GUI-less)

Tool

Text Comparer

Description

This utility checks if two input text files are identical, up to white space differences. Used in various projects. In Unix use "diff" instead.

Test Scripts

(A GUI-less, command-level program)

Translating

The supplied software tools are designed to be run from your computer's command-line environment (also known as "terminal", or "shell"). Command-line environments vary from one operating system to another, and working in them requires some knowledge of various OS shell commands.

In order to eliminate this overhead, we supply batch files (for Windows) and scripts (for Unix and Mac OS), developed by Mark Armbrust. These batch and script files enable invoking the supplied nand2tetris tools from the command line on your computer, painlessly. They can be used from any folder on your computer, without requiring full paths to the files on which they operate. Further, they accept spaces in folder and file names, so they will work if nand2tetris is installed under a folder named, say, "My Documents".

Mac and Linux users

Before running the scripts, you must first change their file attributes to include "executable". You can then run the scripts by typing their name, as well as the .sh extension, in the terminal environment.

If you want to avoid typing the 'sh' extensions, you can create (once and for all) symbolic links in your ~/bin folder. Here is an example how to do it for, say, the HardwareSimulator tool:

ln -s ~/nand2tetris/tools/HardwareSimulator.sh HardwareSimulator

chmod +x HardwareSimulator

Windows users

For the batch files to work from the command line, you must add (once and for all) the nand2tetris/tools folder to your PATH variable.

To run a batch file from command-line, type its name, without the .bat extension.

If you use Windows 7 64-bit you need to install the 64-bit version of Java so that 64-bit cmdexe can run Java commands in batch files. If you get the output "'java' is not recognized..." you likely only have the 32-bit Java installed on your computer.

You can create desktop icons and use them to invoke the interactive versions of the following supplied tools: HardwareSimulator, Assembler, CPUEmulator and VMEmulator. This can be done by finding the disk locations of the respective batch files, right-clicking on them and picking "Send to > Desktop." Edit the shortcuts' properties and set "Run" to "minimized."

### Usage

###

Hardware Simulator: To invoke the hardware simulator in interactive mode, type "HardwareSimulator" in the command line. For example:

C:\...\projects\02> HardwareSimulator

(a window will open up, running the interactive version of the Hardware Simulator)

To invoke the hardware simulator in batch (shell/cmd) mode, type "HardwareSimulator" in the command line. For example:

C:\...\projects\02>HardwareSimulator ALU.tst

(invokes the simulator, loads the given test script, executes it, and reports the result). Note that the simulator's interactive mode also enables loading and executing test scripts.

Successful test (example):

C:\...\projects\02> HardwareSimulator ALU.tst

End of script - Comparison ended successfully

Failed test (example):

C:\...\projects\02> HardwareSimulator ALU.tst

Comparison failure at line 24

Error in the associated HDL file:

C:\...\projects\02> HardwareSimulator ALU.tst

In HDL file C:\...\projects\02\ALU.hdl, Line 60, out[16]: the specified sub bus is not in the bus range: load ALU.hdl

CPU Emulator and VM Emulator: The operations of these tools follow the same convention described above. If you invokve either tool without a parameter, the tool will work in interactive mode; if you supply a parameter (test script), the tool will run batch-style.

Assembler: Typing "Assembler" will start the supplied assembler in interactive mode. Typing "Assembler xxx.asm" will assemble the specified xxx.asm file and generate a file named xxx.hack, containing the translated binary code. Note that the assembler's interactive mode also enables loading and translating .asm files.

Successful assembly (example):

C:\...\projects\04\fill> Assembler Fill.asm Assembling "c:\...\projects\04\fill\Fill.asm"

Failed assembly (example):

C:\...\projects\04\fill> Assembler Fill.asm

Assembling "C:\...\projects\04\fill\Fill.asm" In line 15, Expression expected

To compare the resulting .hack code file to some expected .hack file, use the supplied TextComparer tool, described below.

Compiler: Typing "JackCompiler fileName.jack" will compile the supplied Jack file. Typing "JackCompiler folderName" will compile all the Jack file in the specified folder. Wildcards are not supported. Examples:

Compile a single file:

C:\...\projects\09\Reflect> JackCompiler Mirrors.jack

Compiling "C:\...\projects\09\Reflect\Mirrors.jack"

Compile a folder named "reflect":

C:\...\projects\09> JackCompiler reflect

Compiling "C:\...\projects\09\reflect"

TextComparer: Compares two given files ignoring white space, and reports success or failure. For example, suppose you run the hardware simulator with some test script and get a comparison failure. If you want, you can then use the TextComparer to investigate the problem:

C:\...\projects\02> HardwareSimulator ALU.tst

Comparison failure at line 24

C:\...\projects\02> TextComparer ALU.cmp ALU.out

Comparison failure in line 23:

|0101101110100000|0001111011010010|1|1|0|0|0|0|0001111011010010|0|0| |0101101110100000|0001111011010010|1|1|0|0|0|0|0001111011010010|0|1|

(Note the line number discrepancy between the reports of the two tools).

Help: In Windows, each batch file accepts a "/?" option that shows its intended usage. In Mac and Unix, use "-h". For example:

C:\...\projects\09>JackCompiler /?

Usage:

JackCompiler Compiles all the .jack files in the current working directory.

JackCompiler directoryName Compiles all the .jack files in the specified directory.

JackCompiler fikeName.jack Compiles the specified Jack file

All the nand2tetris software tools are written in Java. If you wish to inspect, modify, or extend some tool, you can [download the source code](https://drive.google.com/file/d/1stcWUSeAixCRHWOjc9sgBhq5voSLvun8/view). Before compiling the source code on your computer, read [Readme.txt](https://www.nand2tetris.org/_files/ugd/44046b_9a0f3b6169c2451b9b37ed62595dc169.pdf).

For details on what's new in the current version of the software (somewhat technical but useful for porting old modifications to the current version), read this [ChangeLog.txt](https://www.nand2tetris.org/_files/ugd/44046b_2a164674985a4d42a7a2770659606f85.pdf) file.

If you wish to share your software extensions with others, please email us at [nand2tetris@gmail.com](mailto:nand2tetris@gmail.com).
