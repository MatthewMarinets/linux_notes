# Linux notes
Tracking all my notes from the jump to linux, and configuration changes I've made.

Mostly for my personal reference, but many troubleshooting steps may be useful to others.
Note I am starting on Linux Mint.

## General
* Linux can type any unicode character with `ctrl+shift+u` + type the unicode hex.
  Hold ctrl+shift while typing the code.
  * `U+AF` makes ¯, U+30C4 makes ツ, for `¯\(ツ)/¯`
  * `U+2122` makes ™

## Knowledge
There seems to be a few ways to install software:
* The system package manager, `apt`
* `.deb` packages, also installed through `apt`
  * These can come from downloads/repositories not in the distro's repository
  * You can automated fetching updates with `curl`
* flatpak, which is managed through the `flatpak` command-line tool
  * Installed at a user-level of system-level
  * Generally less-used, so `flatpak list` is reasonable to read
* snap, which Linux Mint doesn't support
