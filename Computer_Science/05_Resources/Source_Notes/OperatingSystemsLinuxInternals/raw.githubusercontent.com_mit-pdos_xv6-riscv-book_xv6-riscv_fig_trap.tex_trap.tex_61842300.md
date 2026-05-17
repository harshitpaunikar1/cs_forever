Title: trap.tex
Mapped Topic: Teaching kernel implementation
Source URL: https://raw.githubusercontent.com/mit-pdos/xv6-riscv-book/xv6-riscv/fig/trap.tex
Source Type: github_official_repo
Trust Score: 96
Fetched At: 2026-04-17T06:55:54+00:00
Mapped From CSE.md Section: Part 1 / Part 2.C

# Content

\begin{tikzpicture}[>=latex]

\tikzset{
lnode/.style={
thick,
text width = 3cm,
align = center,
}
}

\node[lnode] at (0, 0) (n0) {User code};
\node[lnode] at (0, -2) (n1) {trampoline\\\lstinline{uservec}};
\node[lnode] at (0, -4.0) (n2) {\lstinline{usertrap}};
\node[lnode] at (0, -6.0) (n3) {syscall\\or device driver};

\node[lnode] at (6, 0) (n4) {User code};
\node[lnode] at (6, -2) (n5) {trampoline\\\lstinline{userret}};

\draw[->] (n0) -- (n1);
\draw[->] (n1) -- (n2);
\draw[->] (n2) -- (n3);

\draw[->] (n5) -- (n4);
\draw[->] (n2) -- (6,-4.0) -- (n5);

\end{tikzpicture}
