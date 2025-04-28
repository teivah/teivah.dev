---
title: Vim Cheat Sheet
description: Vim Cheat Sheet
hide:
- navigation
- footer
---

## Action

### Insert + move to insert mode
- `i`: Before the cursor
- `a`: After the cursor
- `s`: Delete the character first
- `I`: Beginning of line
- `A`: End of line
- `o`: New line below
- `O`: New line above
- `gi`: Inserts at the same place at last position
- `{count}s`: Substitute {count} characters

### Selection

NOTE: We can apply each motion to expand the selection

- `i{textobject}`: Select inside block `{textobject}`; e.g., i" (i for inside)
- `a{textobject}`: Select around block `{textobject}`; e.g., a" (a for inside)

Objects: () {} [] <> " ' w p // Paragraph

### Delete/Change/Copy (also copies to the unnamed register)

- `d / c / y`: Delete / change / copy
- `C`: Change until end of line

#### Line

- `dd` / `cc` / `yy`: Current line
- `{action}^`: Beginning of line
- `{action}$` or `{ACTION}`: End of line

#### Word

- `{action}i{textobject}`: Inside block `{textobject}`; e.g., i"
- `{action}a{textobject}`: Around block `{textobject}`; e.g., a"
- `{action}w/{agtion}ge`: Beginning of next word / End of previous word
- `{action}t{char}`: Until `{char}` - not including
- `{action}f{char}`: Until `{char}` - including

#### Delete current character

- `x`: Current character

### Replace

- `r`: Replace a single char
- `R`: Keep replacing

### Count

- `{int}{cmd}`: Repeat {int} times {cmd}

Rule: don't count if you can repeat

### Other

- `>>/<<`: Indent
- `J`: Join next line
- `r<enter>`: Split a line (must be done on a whitespace)

## Motion

### Move

- `w / b`: Forward / backward a word (start of the word)
- `W / B`: Forward / backward a WORD (no whitespace)
- `e / ge`: Forward / backward a word (end/before the word)
- `^ or 0 / $`: Beginning/end of line
- `( )`: Forward / backward a sentence
- `{ }`: Forward / backward a paragraph
- `[{ / ]}`: Beginning/end of a code block
- `[/]m`: Previous/next method

### Jump

- `gg`: First line of file
- `G`: Last line of file
- `g↓/↑/$/0`: Go to the line below/above/end/beginning (when line is wrapped)
- `gv`: Select again the last selected text
- `{int}G`: Go to line {int}
- `5↓`: Move 5 lines below
- `5↑`: Move 5 lines above
- `%`: Matching parenthesis/bracket
- `ctrl+o/i`: Move back / forth in jumplist
- `:ju`: List jumps

### Scan

- `f/F{char}`: Move to the next/previous {char}
- `t/T{char}`: Character before the next/previous occurrence of {char}
- `;/,`: Repeat/reverse

### Easymotion

- `{leader}{leader}w/b`: Start of words forward / backward
- `{leader}{leader}s`: Find a char anywhere

### Sneak

- `s{char1}{char2}`: Find for the next occurrence of {char1}{char2}
- `S{char1}{char2}`: Find backwards
- `;/,`: Next / previous

### Text objects

- `(` `)` b: Parenthesis
- `{` `}` B: Brace
- `]`: Bracket
- `<` `>`: Angle bracket
- `'`: Single quote
- `"`: Double quote
- `at`: Tag (<html>)
- `w`: Word
- `W`: WORD (with space)
- `s`: Sentence
- `p`: Paragraph

### Screen

- `ctrl+e``ctrl+y`: Scrolling down / up one line
- `ctrl+d`/`ctrl+u`: Scrolling down / up half a screen
- `zz`/`zt`/`zb`: Center / top / bottom screen on current line
- `H`/`M`/`L`: Jump to top / middle / bottom of the screen
- `ctrl+f`/`ctrl+b`: Next / previous page

### Word

- `*`: Search the next occurrence of the current word (variable, function, etc), then use n/N to navigate between the matches

## Screen

### Split

- `ctrl+w s/v`: Split down/right
- `ctrl+w {arrow}`: Focus on tab to the left / right / above / below
- `ctrl+w c`: Close window
- `ctrl+w o`: Close others

### Resize

- `ctrl+w =`: Equalize
- `{int} ctrl+w _/|`: Set height/width to {int} rows/columns

## Yank (also copies to the unnamed register)

- `p`: Put after cursor
- `P`: Put before cursor
- `yyp`: Duplicate the line
- `ddp`: Move line after
- `xp`: Move char after


### Register

By default, we use the unnamed register (""). E.g.: dd deletes and puts to the "" register>

- `"{char}{action}`: Puts to the {char} register
- `"{char}p`: Put the {char} register (""p = p)

### History

- `:reg`: Reveal registers history
- `"{int}p`: Paste {int}th previous
- `"0p`: Yank, delete => paste the yanked test

## Macros

- `q{char}`: Start macro {char}
- `q`: Stop macro
- `@{char}`: Play the macro {char}
- `@@`: Play the last macro
- `5@@`: Play 5 times the last macro

NOTE: A macro executed in series is safe, for example if we press fX but X isn't found, the macro stops. To overcome that, we can execute macros in parallel.

- `V (select) :normal @@`: Execute the macro once for each line in the selection
- `q{CHAR}`: Append to the macro {char}

## Search

- `/{text}`: Forward
- `?{text}`: Backward
- `n/N`: Next/previous
- `*`: Go to next/previous occurrence of the current word
- `\c/{text}`: Case insensitive
- `\C/{text}`: Case sensitive

## Other

### Actions

- `u`: Undo
- `ctrl+r`: Redo
- `.`: Repeat

### Navigation

- `:e .`: Open file explorer for the current working directory (edit)
- `:E .`: Open file explorer for directory of the active buffer (explore)
- `:e {file}`: Edit {file}

### Suspend

- `ctrl+z`: Suspend vi
- `fg`: Resume

### Insert text at the end of a group of lines

- `V` select the lines, `:norm A{text}`

### Case

select -> `u/U{textobject}`: Lowercase/Uppercase until text object

## Commands

### Substitute

- `:s/foo/bar`: Substitute foo to bar (line)
- `:s/foo/bar/g`: Substitute all foo occurrences to bar (line)
- `:%s/foo/bar/g`: Substitute all foo occurrences to bar (file)
- `:.,.+4s/foo/bar/g`: Substitute on this line and the next 4 lines

Or `&` to repeat the same command

Or `ctrl+v` to enter visual mode and select the line before executing the cmd

### Global commands

`:g/foo/d`: Delete all lines containing foo
`:g/foo/j`: Join into one line
`:v`: Non-matching lines

### Other

- `:changes`: List the changes
- `:! {cmd}`: Run terminal command