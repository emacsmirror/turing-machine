
# Table of Contents

-   [turing-machine](#org2cd3064)
    -   [Usage](#org2c24606)
        -   [Syntax](#org33d7ada)
        -   [Python](#org5d4a02c)
        -   [Emacs](#org97ad963)
    -   [Emacs Installation](#org40f33bb)
    -   [Todo](#org601b1f2)



<a id="org2cd3064"></a>

# turing-machine

[![img](https://melpa.org/packages/turing-machine-badge.svg)](https://melpa.org/#/turing-machine)
[![img](https://stable.melpa.org/packages/turing-machine-badge.svg)](https://stable.melpa.org/#/turing-machine)
[![img](https://img.shields.io/badge/license-GPL_3-green.svg)](https://www.gnu.org/licenses/gpl-3.0.txt)

Implementation of a single tape turing machine simulator in emacs-lisp and
python (separately).

Inspired by <http://morphett.info/turing/turing.html>


<a id="org2c24606"></a>

## Usage


<a id="org33d7ada"></a>

### Syntax

The syntax for turing code is described in the link above, but for redundancy:

> Syntax:
> 
> -   Each line should contain one tuple of the form `<current state> <current symbol> <new symbol> <direction> <new state>`.
> -   You can use any number or word for `<current state>` and `<new state>`, eg. `10`, `a`, `state1`. State labels are case-sensitive.
> -   You can use any character for `<current symbol>` and `<new symbol>`, or `_` to represent blank (space). Symbols are case-sensitive.
> -   `<direction>` should be `l`, `r` or `*`, denoting 'move left', 'move right' or 'do not move', respectively.
> -   Anything after a `;` is a comment and is ignored.
> -   The machine halts when it reaches any state starting with `halt`, eg. `halt`, `halt-accept`.
> 
> Also:
> 
> -   `*` can be used as a wildcard in `<current symbol>` or `<current state>` to match any character or state.
> -   `*` can be used in `<new symbol>` or `<new state>` to mean 'no change'.
> -   `!` can be used at the end of a line to set a breakpoint, eg `1 a b r 2 !`. The machine will automatically pause after executing this line.
> -   You can specify the starting position for the head using `*` in the initial input.

The <./examples> directory should contain relevant examples. Source should be
listed near the top when not my own.


<a id="org5d4a02c"></a>

### Python

Write a file with the syntax above, and pass it to the script as indicated
below. This is in Python 3. It should be pretty trivial to implement in
python 2.

    Usage:
      turing_machine.py FILENAME INITIAL
      turing_machine.py FILENAME INITIAL [-r|--rate] [RATE]
    
    Options:
      -h --help
      -r --rate  specify delay rate


<a id="org97ad963"></a>

### Emacs

-   Write a file/buffer with the syntax described above, and run
    `turing-machine-execute` to run the simulator.
-   Add `-*- mode: turing-machine -*-` to the top of the file to automatically
    start in `turing-machine-mode` when you next open the file.
-   In `turing-machine-mode` you can press `C-c C-c` (`turing-machine-execute`) to start the machine.
-   Within the code file, you can use `;; INITIAL: [Some initial state]` to denote
    the initial state and `;; RATE: [some number]` to denote the update rate
    in seconds.
    -   If intial state is not set, you will be prompted for it through the
        minibuffer. To be prompted anyway, call `turing-machine-execute` with a
        prefix argument `C-u`.
    -   If rate is not set, it will default to the fastest speed (this is still
        pretty slow). With a double prefix argument `C-u C-u`, you will be prompted
        for rate through the minibuffer
-   Spaces are allowed in initial input, but surrounding spaces are trimmed. You
    can be explicit with `_`.
-   You can choose to hide visualization of spaces with an underscore by setting
    `turing-machine-visual-spaces` to `nil`.


<a id="org40f33bb"></a>

## Emacs Installation

This package is on Melpa. To install using [use-package](https://github.com/jwiegley/use-package):

    (use-package turing-machine
      :ensure t)

Using [quelpa-use-package](https://github.com/quelpa/quelpa-use-package):

    (use-package turing-machine
      :quelpa (turing-machine
               :fetcher github
               :repo "therockmandolinist/turing-machine"))

Or [quelpa](https://github.com/quelpa/quelpa):

    (quelpa '(hacker-typer
              :fetcher github
              :repo "therockmandolinist/turing-machine"))

Otherwise, download the files to somewhere on your load path, and enable
turing-machine:

    (require 'turing-machine)


<a id="org601b1f2"></a>

## Todo

-   Better syntax highlighting.
-   Get rid of cursor in `*turing-machine*` buffer.
-   File extension

