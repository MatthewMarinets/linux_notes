# Audio
The default sound system seems to be pulseaudio.
I've also seen pipewire and alsa thrown around and I'm still learning the difference.

I think Alsa is the API and Pipewire and PulseAudio are different servers?

## Fixing occasional fade-in
By default, pulseaudio enters a power saving mode when audio output has been idle too long.
This means it has to start back up when it needs to output again, and that's noticeable as a ~1s fade-in.

To fix it, disable the power-saving feature.
In `/usr/share/wireplumber/main.lua.d/50-alsa-config.lua`:
* Uncomment the property `session.suspend-timeout-seconds` (near the bottom)
* Set the property to 0
* Restart alsa
  * `sudo /etc/init.d/alsa-utils restart`
  * or Reboot
