# Archipelago on Linux
* Python venv is required
  * `sudo apt install python3-venv`
  * `python -m venv venv`
  * `source venv/bin/activate`
* Run setup.py to get dependencies
* Get sc2 launch script from [lutris](./lutris.md#usage)
  * Script went to `sc2client.sh`
* Replace `cd` and `gamemoderun` commands in bottom of script with the following:
```sh
export SC2PF=WineLinux
export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python
export SC2PATH="/home/matthew/Games/battlenet/drive_c/Program Files (x86)/StarCraft II/"

python3 ./Launcher.py "Starcraft 2 Client" -- $@
```

Launch with `./sc2client.sh`.

Remember to `/download_data`!

## Troubleshooting
### Running script fails, "Permission denied"
* Explanation: You didn't set the "executable" permission on the script
* Fix: run `chmod +x sc2client.sh`

### Connection failing in loop, "argument should be a str or an os.PathLike object [...]
* Symptom: error loop on connection with error message:
  * `argument should be a str or an os.PathLike objhect where __fspath__ returns a str, not 'NoneType'`
* Explanation: Environment variable `SC2PATH` is not defined
* Fix: Ensure `SC2PATH` is defined and points to `Starcraft II` folder in Wine files directory

### Can't open map: Critical error during loading process. Required library d3d9.dll does not exist
* Explanation: cant find file d3d9.dll
* Fix: Removing `d3d9` from `WINEDLLOVERRIDES` in the startup script fixed the issue for me

### sc2 hanging on mission exit with F10 -> d -> q (menu -> end game -> quit)
* Symptom: leaving the game with F10+d+q causes the game to blackscreen but not close
* Fix: unknown
* Exiting with alt+F4 closes fine
  * Can also alt+F4 when the game is already blackscreened
