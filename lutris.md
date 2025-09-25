# Lutris
## Install
* [Downloads page](https://lutris.net/downloads/)
* [Download link](https://github.com/lutris/lutris/releases)
* Install from .deb package
  * `sudo apt install lutris_0.5.18_all.deb`

## Usage
Go to a lutris page and click install. It will open in Lutris

To get a script, run
```sh
# list gameids
lutris -l
lutris lutris:rungameid/$ID --output-script scriptname.sh
```
Where `$ID` is the ID of the game you want a script for

## Adjustments
### Battle.net
* Battle.net was broken -- the .exe was installed in the wrong location
* Added a symlink `~/Games/battlenet/drive_c/Program Files (x86)/Battle.net`
  -> `~/Games/battlenet/Battle.net`
* Got a newer version of wine through ProtonPlus: `wine-10.15-staging-tkg-amd64`

### Starcraft II
* Game options -> Executable: Pointed at SC2Switcher instead of Starcraft II

### Warcraft III World Editor
* Runner options -> Enable VKD3D: Off

