# Compleat/Complgen Syntax for VSCode

![https://github.com/Moenupa/complgen-syntax](https://img.shields.io/badge/Moenupa/complgen--syntax-2B3137?logo=github)
![https://marketplace.visualstudio.com/items?itemName=moenupa.complgen-syntax](https://vsmarketplacebadges.dev/version/moenupa.complgen-syntax.svg)
![https://marketplace.visualstudio.com/items?itemName=moenupa.complgen-syntax](https://vsmarketplacebadges.dev/downloads-short/moenupa.complgen-syntax.svg)

Syntax highlight for [compleat][compleat]/[complgen][complgen],
a unified completion generation language for multiple shells such as bash, zsh, fish and powershell.

[compleat]: https://github.com/mbrubeck/compleat
[complgen]: https://github.com/adaszko/complgen

## Syntax

We prioritize syntax highlighting **complgen** grammars,
due to its active development and extended features over **compleat**.
We describe the implemented syntax rules derived from `complgen@v0.10.1` from
[README][complgenreadme], with `[CG]` denoting features specific to **complgen**:

[complgenreadme]: https://github.com/adaszko/complgen#readme

A _usage_ file `*.usage` contains commands and definitions, separated by semicolons.

A _command_ consists of a command name followed by a pattern. The command name can be any atom. If there is more than one command in the file, we will attempt to match each of them against the input line.

An _atom_ consists of letters, numbers, and any of the characters `_-`, starting with a letter or underscore.

- Any atom matches itself: `foo` matches the string `foo`.
- `a b` matches `a` followed by `b`.
- `a b | c` matches either `a b` or `c`.
- `[a]` matches zero or one occurrences of `a`.
- `a...` matches one or more occurrences of `a`
- `[a]...` matches zero or more occurrences of `a`.
- [CG] `(a | b || c)` shows `a` and `b` as candidates, and `c` only when current input matches neither
  `a` nor `b`. `||` behaves exactly like `|` when matching, it differs only when offering completions.

Use parentheses to group patterns:

- `a (b | c)` matches `a` followed by either `b` or `c`.
- `(a | b) ...` matches `a` or `b` followed by any number of additional
  `a` or `b`.

Variables and Constants:

- A variable can be defined with `<FOO> = bar` and referenced as `<FOO>`.
- [CG] A special variable `<_>` matches any shell word.
- [CG] Predefined variables (default constants, though overridable):
  `<PATH>` and `<DIRECTORY>` match file and directory paths, respectively.
- `<USER@bash>` and `<USER@fish>` define the `<USER>` variable, but are shell-specific.

## Attribution

Syntax based on [complgen grammar][complgengrammar] by [Adam Szkoda][adaszko].

[complgengrammar]: https://github.com/adaszko/complgen
[adaszko]: https://github.com/adaszko

Icon from <a href="https://www.flaticon.com/free-icons/keyboard-key" title="keyboard-key icons">Keyboard-key icons created by littleicon - Flaticon</a>.
