# Ackonwledgements
I would like to thank to the authors of the following repos for their hard work:
https://github.com/Arkq/bluez-alsa
https://gist.github.com/mill1000/74c7473ee3b4a5b13f6325e9994ff84c

I'm building in on top of files provided by them

# Befor we start 
Befor we start, ensure yourself that you have BT capable device, RPi3 or any other RPi with BT dongle and basic bluetooth libraries installed and MPD command line client called `mpc`.

# Bluealsa.service 
This is a proxy that channels the bluetooth intput to the alsa, ie. the sound output.
The location of the bluealse file after install was: 
```
/lib/systemd/system/bluealsa.service
```
And the file contents looks as follows:
```
[Unit]
Description=BluezALSA proxy
Requires=bluetooth.service
After=bluetooth.service

[Service]
Type=simple
User=root
ExecStart=/usr/bin/bluealsa

```

In order to make the a2dp sink working we need to add the proper flags just to be sure
`bluealsa -i hci0 -p a2dp-sink`

# A2DP-agent
This file is attached, it's original state is in the init commit, I'm edditing it to be sure that before some device over bluetooth tries to play somethin, that it stops MDP (in my particular case Mopidy) to free up the physical device to be available for playing some sounds.
This repo helped me with monitoring that there is no device connected and I can shut the service down.
https://github.com/pauloborges/bluez/blob/master/test/monitor-bluetooth

# A2DP-playback.service
I did some minor tweeks for make it work on my particular setup, ie. changed the number of physical HW - the audio card, and added some random delays and buffers I found on the internet to shrink the delay is much as I could.

# Conlusion
In my particular case the whole thing is running on RPi 2 with RaspiDAC attached. The A2DP sink needs some fiddling for the buffering and I guess that the combination of rather slow RPi and external audio card make it even worse ¯\_(ツ)_/¯

But in the end it's working and I can watch youtube videos or anything else on a big screen with decent sound.