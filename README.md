# Bluealsa 
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
