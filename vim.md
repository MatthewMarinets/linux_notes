# vim
Vim is a simple text editor that runs in terminal.
It is usable entirely with keyboard (no mouse).
To allow meta-changes (e.g. save, exit, shortcuts) as well as regular typing, it uses different "modes".

## Type stuff
Press `a` to enter "append" mode.
This mode allows for "normal" typing where characters get inserted at the cursor.

Press `escape` to exit append mode.

## Save/exit
These commands are often preceded by a `:`, and can be combined.
* `:q` quits (will warn of unsaved changes)
* `:w` saves / "writes"
* `:wq` save-and-quit
* `:x` alias for save-and-quit (minor difference: only writes if changes were made)
* `:q!` quits without saving

## Help
* `:help` brings up a general help page
* `:help <key/command>` gives more specific help on what `key/command` does
* `ctrl+O` to exit the help / go back one level if nested

## Navigation ("vim motions")
* Move with arrow keys or hjkl
```
  k
h   l
  j
```
* `w` goes to the start of the next word
* `e` goes to the next end fo the word
* `b` goes back a word (previous start-of-word)
* `f<char>` goes to the next occurrence of `<char>` on the line

## Copy-paste
In general mode:
* `yy` copies a line
* `p` pastes a line
* `dd` deletes (cuts) a line
* `"_dd` deletes a line without affecting clipboard
  * (cut line, but directing clipboard to the "null" register)
