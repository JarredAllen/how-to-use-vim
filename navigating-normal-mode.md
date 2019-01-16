# Navigating Normal Mode

This tutorial assumes that you've already read my [introduction to using vim
for beginners](./a-complete-introduction.md), or are otherwise familiar with
its concepts. Read that document first, if you haven't already.

This document also assumes that the reader is at least vaguely familiar with
regular expressions. If you are not, then there is a sufficient overview of them
[here](https://www.regular-expressions.info/quickstart.html) which you may read.

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
`#` (the # character, not a number) will immediately search for the previous
occurence of whichever word is under the cursor.

There are also movement commands for going to a specific letter. `fc` will move
the cursor to the next occurence of `c` on the given line, while `tc` will move
the cursor to one character before. `F` and `T` act like `f` and `t`, except
that the upper-case letters tell vim to search for the previous occurence of
the letter instead of the next one.

There are shortcuts for moving to specific lines. `#G` (where # is a number)
will move the cursor to the beginning of the specified line number. `gg` will
move the cursor to the beginning of the entire document. `G` (without a number
preceeding it) will move the cursor to the beginning of the last line of the
document.

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

Pressing `a` is like `i` except, instead of inserting before the character which
the cursor is over, it appends to after the location.

Using `I` and `A` (upper-case) can be used to move to enter insert mode at either
the beginning or end of the current line, respectively. They are analogous to
`^i` and `$a`.

Using `c` allows you to simultaneously remove some text and switch to insert
mode. To do this, type c and then a movement command. Whatever is between the
cursor location before executing the command and after executing the command
gets erased. For example, `c$` replaces the rest of the line, `cG` replaces the
rest of the document, `c5w` replaces the next 5 words, etc. `cc` can also be
used, to erase the entire line and go into insert mode (analogous to `^c$`).

### Editing the document from Insert Mode

From insert mode, you can type in text onto the document. However, normal mode
also provides powerful tools for editing documents which you can use.

##### Cutting text

Typing `d` can be used to cut text from the document. If you type `dd`, then it
deletes the entire line, and `d#d` deletes that many lines starting from the
current one. If `d` is instead followed by a movement command, then it deletes
from the cursor location to the cursor's final location. For example, `d$` will
delete the rest of the line, and `d^` will delete everything before the cursor.

You can also type `x` to cut the character currently underneath the cursor,
or `#x` to cut a specific number of characters.

##### Copy/Paste

Vim also supports copying and pasting text.

To copy text, type `y` and then a movement command. The text over which the
cursor moves will then be copied. Alternatively, you can type `yy` to copy the
entire current line.

To paste text, type p. This will paste the text after the cursor. If the text
being pasted contains no line breaks, it will be placed immediately following
the cursor. If there are line breaks in the text, then it will be placed below
the cursor, in new lines immediately following the current.

Any text which is deleted through the use of the `c`, `d`, or `x` commands will
automatically be copied. To avoid this, type `"_` (a double-quote then an
underscore) before the `c` or `d`. For why this works, read the article on
registers when I write it.

##### Indenting Text

You can use `>` to indent lines of text. If you type `>`, followed by a movement
command, then any line between the cursor's initial and final position will be
indented one more time. Like with other commands, `>>` can be used to indent
the current line more, and `>#>` can be used to indent a specific number of
lines of text, starting at the cursor. You can also use `<` similarly, to remove
indentation instead of adding it.

You can also use `=` to have vim guess at the correct indentation. It functions
similarly to `<` and `>`, except it tries to figure out the "correct"
indentation (if you're writing code, it will base that on the language's
preferred style rules) and makes all lines have that. `gg=G` will have vim try
to correct the indentation on every line in the file.

## Where to from here

While this document does not describe everything which may be done from the
command-line mode, it does describe a large number of things. If you've read
and practiced everything described here, then you may consider yourself
proficient at what can be done from normal mode.

There are several features described here where I only brush the surface, such
as copying and pasting text. In the future, I will have documents up describing
those systems in much greater detail.

I will also have a chapter describing the command-line mode in more detail.

