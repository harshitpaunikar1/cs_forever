Title: Comments - cppreference.com
Mapped Topic: C++ reference
Source URL: https://en.cppreference.com/w/cpp/comments.html
Source Type: reference_docs
Trust Score: 90
Fetched At: 2026-04-17T07:07:06+00:00
Mapped From CSE.md Section: Part 2: D. Programming / coding stack

# Content

# Comments

[cpp](https://en.cppreference.com/cpp.html)

Comments serve as a sort of in-code documentation. When inserted into a program, they are effectively ignored by the compiler; they are solely intended to be used as notes by the humans that read source code. Although specific documentation is not part of the C++ standard, several utilities exist that parse comments with different documentation formats.

## Contents |

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/comment&action=edit§ion=1)] Syntax

comment
|
(1) | ||||||||
comment
|
(2) | ||||||||

All comments are removed from the program at [translation phase 3](https://en.cppreference.com/language/translation_phases.html#Phase_3) by replacing each comment with a single whitespace character.

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/comment&action=edit§ion=2)] C-style

C-style comments are usually used to comment large blocks of text, however, they can be used to comment single lines. To insert a C-style comment, simply surround text with

and **/***

; this will cause the contents of the comment to be ignored by the compiler. Although it is not part of the C++ standard, ***/**

and **/****

are often used to indicate documentation blocks; this is legal because the second asterisk is simply treated as part of the comment. C-style comments cannot be nested.
***/**

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/comment&action=edit§ion=3)] C++-style

C++-style comments are usually used to comment single lines, however, multiple C++-style comments can be placed together to form multi-line comments. C++-style comments tell the compiler to ignore all content between

and a new line.
**//**

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/comment&action=edit§ion=4)] Notes

Because comments [are removed](https://en.cppreference.com/language/translation_phases.html#Phase_3) before the preprocessor stage, a macro cannot be used to form a comment and an unterminated C-style comment doesn't spill over from an #include'd file.

Besides commenting out, other mechanisms used for source code exclusion are

#if 0[std::cout]<< "this will not be executed or even compiled\n"; #endif

and

if (false) {[std::cout]<< "this will not be executed\n"; }

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/comment&action=edit§ion=5)] Example

#include <iostream> /* C-style comments can contain multiple lines */ /* or just one */ /************** * you can insert any *, but * you can't make comments nested */ // C++-style comments can comment one line // or, they can // be strung together int main() { // comments are removed before preprocessing, // so ABC is "1", not "1//2134", and "1 hello world" // will be printed #define ABC 1//2134[std::cout]<< ABC << " hello world\n"; // The below code won't be run // return 1; // The below code will be run return 0; }

Output:

1 hello world

### [[edit](https://en.cppreference.com/mwiki/index.php?title=cpp/comment&action=edit§ion=6)] See also

|
|
