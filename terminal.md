# Terminal
Noting useful terminal commands

## Locating executables
There's nothing _quite_ like Windows's `where` command,
which locates _all_ instances of a executable file on the path,
where the first is the one actually executed.

### type -p `<filename>`
* This searches only on the path
* Returns only one path

### which `<filename>`
* Only returns 1 result
* Only works for binaries, not scripts

### locate `<filename>`
* Finds the absolute path location of `<filename>`.
* Doesn't filter by what's on the path
* Uses a database updated by `updatedb` -- faster, but may be inaccurate if db is out of date

### find `<startdir>` -name `<filename>`
* General file search
* Doesn't filter by what's on the path
* Searches filesystem, but slower than `locate`
