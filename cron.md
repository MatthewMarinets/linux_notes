# Cron
`cron` is used to schedule tasks.

Note the @reboot time runs before the desktop environment is initialized;
to run scripts when the desktop is started, see what I did in
[Keyboard/mouse configuration](./keyboard_mouse.md#scheduling-script-on-startup).

## View
```sh
crontab -l
```

## On startup
```sh
# make a script
mkdir ~/startup
cd ~/startup
touch ./script.sh
chmod +x /script.sh

# schedule it
crontab -e
@reboot /home/startup/script.sh
```
