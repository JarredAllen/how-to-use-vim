# Navigating Normal Mode

This tutorial assumes that you've already read my [introduction to using vim
for beginners](./a-complete-introduction.md), or are otherwise familiar with
its concepts. Read that document first, if you haven't already.

This document also assumes that the reader is at least vaguely familiar with
regular expressions. If you are not, then there is a sufficient overview of them
[here](https://www.regular-expressions.info/quickstart.html) which you may read.

**Work in Progresss** This document is far from complete.

## Overview of Normal Mode

One difference about normal mode in vim is that the cursor is over a character,
not between characters. This means that there will always be a character under
the cursor, which appears as highlighted while using normal mode.

### Navigating Your Document

You can move the cursor around the document using the arrow keys. However,
the arrow keys are far from the rest of the keyboard and limited in their
abilities, so vim provides other methods.

The basic navigation keys are `h`, `j`, `k`, and `l`, corresponding to left,
down, up and right, respectively. These keys have the same functionality, but
are on the home row, instead of being off to the side, away from all the other
keys you want to press.

A warning: all of the commands listed in this chapter are to be done directly
within normal mode. Do not enter insert mode, and do not type `:` to enter
command-line mode.

Those four keys were chosen because the computer on which vi (a predecessor
of vim) was written reused those letters as the arrow keys (a picture of the
kayboard is pasted below).

![Original Vim Keyboard](./images/vim-hjkl-keyboard.jpg)

Try navigating around in normal mode using those keys, on any text document of
your choice. It'll take some getting used to, but you'll eventually be faster
at using those keys than with the arrow keys.

There are other movement commands you can do:

For moving within a given line, `^` and `$` will take you to the
beginning and end of the current line (ignoring whitespace), while `0` will take
you to the very beginning, before any leading whitespace.

Also, `+` and `-` will take you to the beginning of the next or previous line,
respectively. They act identically to the sequences `j^` and `k^`.

There are also some movements commands which move you across words.
`w` will take you to the beginning of the next word. `e` will take you to the
end of the current word. `b` will take you to the beginning of the current word
(or to the previous one if you're already at the beginning). Using lower case
letters (`w`, `e`, and `b`) will count punctuation or whitespace as word
delimiters (i.e. the string "some-text" is split across the dash), while using
upper-case letters (`W`, `E`, and `B`) will only separate words with whitespace
(so "some-text" is one word but "some text" is two).

You can also move through the document by searching for text. Typing `/{text}`,
where {text} is the text you want to search for, will search through the
document and move the cursor to the next occurence of the regular expression
specified by {text}. `?{text}` does likewise, but searches backwards from the
cursor instead of forward. After searching for text, you can use `n` to find the
next result (in the original direction of the search) or `N` to find the
previous (searching the opposite direction as the used command) result. Typing
`#` will immediately search for the previous occurence of whichever word is
under the cursor.

There are also movement commands for going to a specific letter. `fc` will move
the cursor to the next occurence of `c` on the given line, while `tc` will move
the cursor to one character before. `F` and `T` act like `f` and `t`, except
that the upper-case letters tell vim to search for the previous occurence of
the letter instead of the next one.

There are shortcuts for moving to specific lines. `#G` will move the cursor to
the beginning of the specified line number. `gg` will move the cursor to the
beginning of the entire document. `G` (without a number preceeding it) will
move the cursor to the beginning of the last line of the document.

You can specify a number before a movement command to repeat that action
multiple times. For example, `5j` will move the cursor down five lines, and
`3b` will skip the current and previous words and go to the beginning of the
word before it.

Lastly, when dealing with parentheses, brackets, etc., you can press `%` while
the cursor is over one to move it to the corresponding one.

### Other ways to enter Insert Mode

Pressing `i` is only one of several ways through which you can enter insert
mode and begin typing text. Vim provides many other methods, each of which
move you into insert mode slightly differently.

### Editing the document from Insert Mode

From insert mode, you can type in text onto the document. However, normal mode
also provides powerful tools for editing documents which you can use.

