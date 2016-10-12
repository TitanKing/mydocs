## KDE 5.5+ Tweaks ##
I find KDE to provide the best experience for a desktop environment. There are a few things that irk me. For instance the fact that GTK (Gnome) applications looks so much different with missing icons and ugly none universal looks. There are a few ways to fix it:

## Oxygen theme
Install the oxygen theme:  
`sudo apt-get install kdeartwork-theme-icon gtk3-engines-oxygen kde-config-gtk-style`

From here in your application style settings (KDE) you can now choose oxygen as both the kde and gnome theme.

## Repo improvements
For a list of later packages than that of the default repo install:
`sudo apt-add-repository ppa:nilarimogard/webupd8`

It includes updates to [See Here](https://launchpad.net/~nilarimogard/+archive/ubuntu/webupd8)

## Media Players
I found Clementine to be the best by far, install from native repo:

`sudo add-apt-repository ppa:me-davidsansome/clementine`

## Fixes

### Vsync issues

```
export __GL_YIELD="USLEEP"
export KWIN_TRIPLE_BUFFER=0
export KWIN_USE_BUFFER_AGE=0
```

Add these lines to etc/profile.d/kwin.sh

### Blackwidow Keyboard Macro Keys Assign

Install the following packages:

`sudo apt-get install libusb-1.0-0 && sudo apt-get install python-usb`

Clone the following script:

`https://github.com/TitanKing/blackwidowcontrol`

Extract package and move the files as follow:

`blackwidowcontrol.py => /usr/bin/blackwidow_enable.py` (For older drivers)

`blackwidowcontrol.py => /usr/bin/blackwidowcontrol.py` (Only For Synapses Driver V2)

`razer_blackwidow.rules => /etc/udev/rules.d/razer_blackwidow.rules` (Only For Synapses Driver V2)

Reboot and after see:
After install (possible reboot) run `xev` in terminal to see if M1-M5 keys work.
[KDEMultimediaKeys](https://wiki.kubuntu.org/KDEMultimediaKeys)

Also see for original help article:
[More Help](http://superuser.com/questions/342107/getting-macro-keys-from-a-razer-blackwidow-to-work-on-linux)

Assigning Keyboard Keys:
Install `sudo apt-get install autokey-qt` or `sudo apt-get install autokey-gtk`
Use autohotkey to assign keyboard shortcuts to M keys. 
Make it startup.
